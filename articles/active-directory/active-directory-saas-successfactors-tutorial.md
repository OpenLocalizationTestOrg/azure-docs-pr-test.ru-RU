---
title: "Руководство по интеграции Azure Active Directory с SuccessFactors | Документация Майкрософт"
description: "Узнайте, как использовать SuccessFactors с Azure Active Directory для реализации единого входа, автоматической подготовки к работе и многого другого."
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
ms.openlocfilehash: e85a38ccbe25263ac42bc76351416b023fb77c87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="afa24-103">Руководство. Интеграция Azure Active Directory с SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="afa24-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="afa24-104">Цель этого руководства — показать, как интегрировать приложение SuccessFactors с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="afa24-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="afa24-105">Интеграция SuccessFactors с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="afa24-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="afa24-106">С помощью Azure AD вы можете контролировать доступ к приложению SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="afa24-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="afa24-107">Вы можете включить автоматический вход пользователей в SuccessFactors (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa24-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="afa24-108">Вы можете управлять учетными записями централизованно — через классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="afa24-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="afa24-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="afa24-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afa24-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="afa24-110">Prerequisites</span></span>
<span data-ttu-id="afa24-111">Чтобы настроить интеграцию Azure AD с SuccessFactors, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="afa24-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="afa24-112">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="afa24-112">A valid Azure subscription</span></span>
* <span data-ttu-id="afa24-113">клиент в SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="afa24-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="afa24-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="afa24-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="afa24-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="afa24-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="afa24-116">Не следует использовать рабочую среду при отсутствии необходимости.</span><span class="sxs-lookup"><span data-stu-id="afa24-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="afa24-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="afa24-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="afa24-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="afa24-118">Scenario description</span></span>
<span data-ttu-id="afa24-119">Цель этого учебника — научить вас проверять единый вход в Azure AD в пробной среде.</span><span class="sxs-lookup"><span data-stu-id="afa24-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="afa24-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="afa24-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="afa24-121">Добавление SuccessFactors из коллекции.</span><span class="sxs-lookup"><span data-stu-id="afa24-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="afa24-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa24-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="afa24-123">Добавление SuccessFactors из коллекции</span><span class="sxs-lookup"><span data-stu-id="afa24-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="afa24-124">Чтобы настроить интеграцию SuccessFactors с Azure AD, необходимо добавить SuccessFactors из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="afa24-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="afa24-125">**Чтобы добавить SuccessFactors из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="afa24-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="afa24-126">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="afa24-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![Настройка единого входа][1]
2. <span data-ttu-id="afa24-128">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="afa24-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="afa24-129">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="afa24-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Настройка единого входа][2]
4. <span data-ttu-id="afa24-131">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="afa24-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Приложения][3]
5. <span data-ttu-id="afa24-133">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="afa24-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Настройка единого входа][4]
6. <span data-ttu-id="afa24-135">В **поле поиска** введите **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="afa24-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![Настройка единого входа][5]
7. <span data-ttu-id="afa24-137">В области результатов выберите **SuccessFactors** и щелкните **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="afa24-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![Настройка единого входа][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="afa24-139">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa24-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="afa24-140">Цель этого раздела — показать, как настроить и проверить единый вход Azure AD в приложении SuccessFactors с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="afa24-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="afa24-141">Для работы единого входа в Azure AD необходимо знать, какой пользователь в SuccessFactors соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa24-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="afa24-142">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="afa24-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="afa24-143">Чтобы установить эту связь, следует указать **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="afa24-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="afa24-144">Чтобы настроить и проверить единый вход Azure AD в SuccessFactors, вам потребуется выполнить действия, описанные в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="afa24-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="afa24-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="afa24-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="afa24-146">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="afa24-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="afa24-147">**[Создание тестового пользователя SuccessFactors](#creating-a-successfactors-test-user)** требуется для создания пользователя Britta Simon в SuccessFactors, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa24-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="afa24-148">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa24-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="afa24-149">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="afa24-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="afa24-150">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa24-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="afa24-151">В этом разделе описано, как включить единый вход Azure AD на классическом портале и настроить его в приложении SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="afa24-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="afa24-152">**Чтобы настроить единый вход Azure AD в SuccessFactors, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="afa24-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="afa24-153">На классическом портале Azure на странице интеграции с приложением **SuccessFactors** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="afa24-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![Настройка единого входа][7]
2. <span data-ttu-id="afa24-155">На странице **Как пользователи должны входить в SuccessFactors?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afa24-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Настройка единого входа][8]
3. <span data-ttu-id="afa24-157">На странице **Настроить URL-адрес приложения** выполните следующие действия и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afa24-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![Настройка единого входа][9]
   
    <span data-ttu-id="afa24-159">а.</span><span class="sxs-lookup"><span data-stu-id="afa24-159">a.</span></span> <span data-ttu-id="afa24-160">В текстовое поле **URL-адрес для входа** введите URL-адрес в любом из следующих форматов:</span><span class="sxs-lookup"><span data-stu-id="afa24-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="afa24-161">b.</span><span class="sxs-lookup"><span data-stu-id="afa24-161">b.</span></span> <span data-ttu-id="afa24-162">В текстовое поле **URL-адрес ответа** введите URL-адрес в любом из следующих форматов:</span><span class="sxs-lookup"><span data-stu-id="afa24-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="afa24-163">c.</span><span class="sxs-lookup"><span data-stu-id="afa24-163">c.</span></span> <span data-ttu-id="afa24-164">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afa24-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="afa24-165">Обратите внимание, что значения, указанные выше, используются в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="afa24-165">Please note that these are not the real values.</span></span> <span data-ttu-id="afa24-166">Необходимо заменить эти значения на фактические URL-адреса для входа и ответа.</span><span class="sxs-lookup"><span data-stu-id="afa24-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="afa24-167">Чтобы узнать эти адреса, обратитесь в [службу поддержки SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="afa24-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="afa24-168">На странице **Настройка единого входа в SuccessFactors** щелкните **Скачать сертификат** и сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="afa24-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Настройка единого входа][10]

2. <span data-ttu-id="afa24-170">В другом окне веб-браузера войдите на **портал администрирования SuccessFactors** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="afa24-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="afa24-171">Откройте раздел **Application Security** (Безопасность приложения) и найдите в нем **функцию единого входа**.</span><span class="sxs-lookup"><span data-stu-id="afa24-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="afa24-172">Введите любое значение в поле **Reset Token** (Сброс маркера) и нажмите кнопку **Save Token** (Сохранить маркер), чтобы включить единый вход SAML.</span><span class="sxs-lookup"><span data-stu-id="afa24-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![Настройка единого входа на стороне приложения][11]

    > [!NOTE] 
    > <span data-ttu-id="afa24-174">Это значение используется только как признак включения.</span><span class="sxs-lookup"><span data-stu-id="afa24-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="afa24-175">Если здесь сохранено любое значение, единый вход SAML включен.</span><span class="sxs-lookup"><span data-stu-id="afa24-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="afa24-176">Если сохранено пустое значение, единый вход SAML отключен.</span><span class="sxs-lookup"><span data-stu-id="afa24-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="afa24-177">Перейдите на экран, представленный на снимке ниже, и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="afa24-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![Настройка единого входа на стороне приложения][12]
   
    <span data-ttu-id="afa24-179">а.</span><span class="sxs-lookup"><span data-stu-id="afa24-179">a.</span></span> <span data-ttu-id="afa24-180">Установите переключатель **SAML v2 SSO** (Единый вход SAML версии 2).</span><span class="sxs-lookup"><span data-stu-id="afa24-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="afa24-181">b.</span><span class="sxs-lookup"><span data-stu-id="afa24-181">b.</span></span> <span data-ttu-id="afa24-182">Задайте имя утверждающей стороны SAML (например, "Издатель SAML + название компании").</span><span class="sxs-lookup"><span data-stu-id="afa24-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="afa24-183">c.</span><span class="sxs-lookup"><span data-stu-id="afa24-183">c.</span></span> <span data-ttu-id="afa24-184">В текстовом поле **SAML Issuer** (Издатель SAML) вставьте значение **URL-адреса издателя** из мастера настройки приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa24-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="afa24-185">d.</span><span class="sxs-lookup"><span data-stu-id="afa24-185">d.</span></span> <span data-ttu-id="afa24-186">Выберите значение **Response(Customer Generated/IdP/AP)** (Ответ (создается клиентом/IdP/AP)) для параметра **Require Mandatory Signature** (Требуется обязательная подпись).</span><span class="sxs-lookup"><span data-stu-id="afa24-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="afa24-187">д.</span><span class="sxs-lookup"><span data-stu-id="afa24-187">e.</span></span> <span data-ttu-id="afa24-188">Выберите значение **Enabled** (Включено) для параметра **Enable SAML Flag** (Включить флаг SAML).</span><span class="sxs-lookup"><span data-stu-id="afa24-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="afa24-189">Е.</span><span class="sxs-lookup"><span data-stu-id="afa24-189">f.</span></span> <span data-ttu-id="afa24-190">Выберите значение **No** (Нет) для параметра **Login Request Signature (SF Generated/SP/RP)** (Подпись запроса на вход (создается SF/SP/RP)).</span><span class="sxs-lookup"><span data-stu-id="afa24-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="afa24-191">ж.</span><span class="sxs-lookup"><span data-stu-id="afa24-191">g.</span></span> <span data-ttu-id="afa24-192">Выберите значение **Browser/Post Profile** (Браузер/пост-профилирование) для параметра **SAML Profile** (Профиль SAML).</span><span class="sxs-lookup"><span data-stu-id="afa24-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="afa24-193">h.</span><span class="sxs-lookup"><span data-stu-id="afa24-193">h.</span></span> <span data-ttu-id="afa24-194">Выберите значение **No** (Нет) для параметра **Enforce Certificate Valid Period** (Применять период действия сертификата).</span><span class="sxs-lookup"><span data-stu-id="afa24-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="afa24-195">i.</span><span class="sxs-lookup"><span data-stu-id="afa24-195">i.</span></span> <span data-ttu-id="afa24-196">Скопируйте содержимое скачанного файла сертификата и вставьте его в текстовое поле **SAML Verifying Certificate** (Сертификат для проверки SAML).</span><span class="sxs-lookup"><span data-stu-id="afa24-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="afa24-197">Содержимое сертификата должно включать открывающий и закрывающий теги сертификата.</span><span class="sxs-lookup"><span data-stu-id="afa24-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="afa24-198">Перейдите в раздел SAML V2 и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="afa24-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![Настройка единого входа на стороне приложения][13]
   
    <span data-ttu-id="afa24-200">а.</span><span class="sxs-lookup"><span data-stu-id="afa24-200">a.</span></span> <span data-ttu-id="afa24-201">Выберите значение **Yes** (Да) для параметра **Support SP-initiated Global Logout** (Поддержка глобального выхода, инициированного SP).</span><span class="sxs-lookup"><span data-stu-id="afa24-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="afa24-202">b.</span><span class="sxs-lookup"><span data-stu-id="afa24-202">b.</span></span> <span data-ttu-id="afa24-203">В текстовом поле **Global Logout Service URL (LogoutRequest destination)** (URL-адрес службы глобального выхода) вставьте значение **URL-адреса удаленного выхода** из мастера настройки приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa24-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="afa24-204">c.</span><span class="sxs-lookup"><span data-stu-id="afa24-204">c.</span></span> <span data-ttu-id="afa24-205">Выберите значение **No** (Нет) для параметра **Require sp must encrypt all NameID element** (Требуется шифрование всех элементов NameID на стороне SP).</span><span class="sxs-lookup"><span data-stu-id="afa24-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="afa24-206">d.</span><span class="sxs-lookup"><span data-stu-id="afa24-206">d.</span></span> <span data-ttu-id="afa24-207">Выберите значение **unspecified** (Не определено) для параметра **NameID Format** (Формат идентификатора имени).</span><span class="sxs-lookup"><span data-stu-id="afa24-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="afa24-208">д.</span><span class="sxs-lookup"><span data-stu-id="afa24-208">e.</span></span> <span data-ttu-id="afa24-209">Выберите значение **Yes** (Да) для параметра **Enable sp initiated login (AuthnRequest)** (Включить вход по требованию SP).</span><span class="sxs-lookup"><span data-stu-id="afa24-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="afa24-210">Е.</span><span class="sxs-lookup"><span data-stu-id="afa24-210">f.</span></span> <span data-ttu-id="afa24-211">В текстовом поле **Send request as Company-Wide issuer** (Отправлять запрос как издатель в пределах компании) вставьте **URL-адрес удаленного входа** из мастера настройки приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afa24-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="afa24-212">Чтобы в именах для входа не учитывался регистр, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="afa24-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="afa24-213">а.</span><span class="sxs-lookup"><span data-stu-id="afa24-213">a.</span></span> <span data-ttu-id="afa24-214">Найдите в нижней части экрана раздел **Company Settings**(Параметры компании).</span><span class="sxs-lookup"><span data-stu-id="afa24-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="afa24-215">b.</span><span class="sxs-lookup"><span data-stu-id="afa24-215">b.</span></span> <span data-ttu-id="afa24-216">Установите флажок **Enable Non-Case-Sensitive Username** (Имя пользователя без учета регистра).</span><span class="sxs-lookup"><span data-stu-id="afa24-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="afa24-217">в) Щелкните **Save**(Сохранить).</span><span class="sxs-lookup"><span data-stu-id="afa24-217">c.Click **Save**.</span></span>
   
    ![Настройка единого входа][29]

    > [!NOTE] 
    > <span data-ttu-id="afa24-219">При попытке включить этот параметр система проверит, не возникнут ли повторяющиеся имена для входа SAML.</span><span class="sxs-lookup"><span data-stu-id="afa24-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="afa24-220">Предположим, что у клиента есть пользователи с именами User1 и user1.</span><span class="sxs-lookup"><span data-stu-id="afa24-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="afa24-221">Если отменить учет регистра, эти имена будут считаться одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="afa24-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="afa24-222">В таком случае система выдаст сообщение об ошибке и параметр не будет включен.</span><span class="sxs-lookup"><span data-stu-id="afa24-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="afa24-223">Клиенту потребуется изменить одно из таких имен пользователя, чтобы они имели различное написание.</span><span class="sxs-lookup"><span data-stu-id="afa24-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="afa24-224">На классическом портале Azure выберите подтверждение конфигурации единого входа, а затем нажмите кнопку **Завершить**, чтобы закрыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="afa24-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![Приложения][14]
2. <span data-ttu-id="afa24-226">На странице **Подтверждение единого входа** нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="afa24-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Приложения][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="afa24-228">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa24-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="afa24-229">Цель этого раздела — создать на классическом портале тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="afa24-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][16]

<span data-ttu-id="afa24-231">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="afa24-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="afa24-232">На **классическом портале Azure** в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="afa24-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Создание тестового пользователя Azure AD][17]
2. <span data-ttu-id="afa24-234">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="afa24-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="afa24-235">Чтобы отобразить список пользователей, в меню вверху выберите **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="afa24-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Создание тестового пользователя Azure AD][18]
4. <span data-ttu-id="afa24-237">Чтобы открыть диалоговое окно **Добавление пользователя**, на панели инструментов внизу нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="afa24-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Создание тестового пользователя Azure AD][19]
5. <span data-ttu-id="afa24-239">На странице диалогового окна **Тип учетной записи пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="afa24-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][20]
   
    <span data-ttu-id="afa24-241">а.</span><span class="sxs-lookup"><span data-stu-id="afa24-241">a.</span></span> <span data-ttu-id="afa24-242">В поле «Тип пользователя» выберите значение «Новый пользователь в вашей организации».</span><span class="sxs-lookup"><span data-stu-id="afa24-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="afa24-243">b.</span><span class="sxs-lookup"><span data-stu-id="afa24-243">b.</span></span> <span data-ttu-id="afa24-244">В текстовом поле **Имя пользователя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="afa24-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="afa24-245">c.</span><span class="sxs-lookup"><span data-stu-id="afa24-245">c.</span></span> <span data-ttu-id="afa24-246">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afa24-246">Click **Next**.</span></span>
6. <span data-ttu-id="afa24-247">На странице диалогового окна **Профиль пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="afa24-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][21]
   
    <span data-ttu-id="afa24-249">а.</span><span class="sxs-lookup"><span data-stu-id="afa24-249">a.</span></span> <span data-ttu-id="afa24-250">В текстовом поле **Имя** введите **Britta**.</span><span class="sxs-lookup"><span data-stu-id="afa24-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="afa24-251">b.</span><span class="sxs-lookup"><span data-stu-id="afa24-251">b.</span></span> <span data-ttu-id="afa24-252">В текстовом поле **Фамилия** введите **Simon**.</span><span class="sxs-lookup"><span data-stu-id="afa24-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="afa24-253">c.</span><span class="sxs-lookup"><span data-stu-id="afa24-253">c.</span></span> <span data-ttu-id="afa24-254">В текстовом поле **Отображаемое имя** введите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="afa24-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="afa24-255">d.</span><span class="sxs-lookup"><span data-stu-id="afa24-255">d.</span></span> <span data-ttu-id="afa24-256">В списке **Роль** выберите **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="afa24-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="afa24-257">д.</span><span class="sxs-lookup"><span data-stu-id="afa24-257">e.</span></span> <span data-ttu-id="afa24-258">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="afa24-258">Click **Next**.</span></span>
7. <span data-ttu-id="afa24-259">На странице диалогового окна **Получить временный пароль** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="afa24-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Создание тестового пользователя Azure AD][22]
8. <span data-ttu-id="afa24-261">На странице диалогового окна **Получить временный пароль** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="afa24-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Создание тестового пользователя Azure AD][23]
   
    <span data-ttu-id="afa24-263">а.</span><span class="sxs-lookup"><span data-stu-id="afa24-263">a.</span></span> <span data-ttu-id="afa24-264">Запишите значение поля **Новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="afa24-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="afa24-265">b.</span><span class="sxs-lookup"><span data-stu-id="afa24-265">b.</span></span> <span data-ttu-id="afa24-266">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="afa24-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="afa24-267">Создание тестового пользователя SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="afa24-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="afa24-268">Чтобы пользователи Azure AD могли выполнять вход в SuccessFactors, они должны быть подготовлены для работы с SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="afa24-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="afa24-269">В случае SuccessFactors подготовка пользователей осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="afa24-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="afa24-270">Чтобы создать пользователей в SuccessFactors, необходимо обратиться в [службу поддержки SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="afa24-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="afa24-271">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="afa24-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="afa24-272">Цель этого раздела — разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="afa24-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![Назначение пользователя][24]

<span data-ttu-id="afa24-274">**Чтобы назначить пользователя Britta Simon в SuccessFactors, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="afa24-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="afa24-275">Чтобы открыть представление приложений, в представлении каталога на классическом портале щелкните **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="afa24-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Назначение пользователя][25]
2. <span data-ttu-id="afa24-277">Из списка приложений выберите **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="afa24-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![Настройка единого входа][26]
3. <span data-ttu-id="afa24-279">В меню в верхней части страницы щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="afa24-279">In the menu on the top, click **Users**.</span></span>
   
    ![Назначение пользователя][27]
4. <span data-ttu-id="afa24-281">В списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="afa24-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="afa24-282">На панели инструментов внизу щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="afa24-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Назначение пользователя][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="afa24-284">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="afa24-284">Testing single sign-on</span></span>
<span data-ttu-id="afa24-285">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="afa24-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="afa24-286">Щелкнув плитку SuccessFactors на панели доступа, вы автоматически войдете в приложение SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="afa24-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="afa24-287">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="afa24-287">Additional resources</span></span>
* [<span data-ttu-id="afa24-288">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="afa24-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="afa24-289">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="afa24-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
