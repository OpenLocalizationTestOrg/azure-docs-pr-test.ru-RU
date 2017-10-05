---
title: "Предварительные требования для доступа к API отчетов Azure AD | Документация Майкрософт"
description: "Узнайте о предварительных требованиях для доступа к API отчетов Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5fafd83c337e3c73260d89cdad7409a01ce5855b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="974c1-103">Предварительные требования для доступа к API отчетов Azure AD</span><span class="sxs-lookup"><span data-stu-id="974c1-103">Prerequisites to access the Azure AD reporting API</span></span>

<span data-ttu-id="974c1-104">[Интерфейсы API отчетов Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) предоставляют программный доступ к данным с помощью набора интерфейсов API на базе REST.</span><span class="sxs-lookup"><span data-stu-id="974c1-104">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="974c1-105">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="974c1-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="974c1-106">API отчетов использует [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) для авторизации доступа к веб-API.</span><span class="sxs-lookup"><span data-stu-id="974c1-106">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="974c1-107">Чтобы получить доступ к данным отчетов через API, необходима одна из следующих ролей:</span><span class="sxs-lookup"><span data-stu-id="974c1-107">To get access to the reporting data through the API, you need to have one of the following roles assigned:</span></span>

- <span data-ttu-id="974c1-108">Чтение данных безопасности</span><span class="sxs-lookup"><span data-stu-id="974c1-108">Security Reader</span></span>
- <span data-ttu-id="974c1-109">администратор безопасности;</span><span class="sxs-lookup"><span data-stu-id="974c1-109">Security Admin</span></span>
- <span data-ttu-id="974c1-110">глобальный администратор.</span><span class="sxs-lookup"><span data-stu-id="974c1-110">Global Admin</span></span>


<span data-ttu-id="974c1-111">Чтобы подготовить доступ к API отчетов, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="974c1-111">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="974c1-112">Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="974c1-112">Register an application</span></span> 
2. <span data-ttu-id="974c1-113">предоставьте разрешения;</span><span class="sxs-lookup"><span data-stu-id="974c1-113">Grant permissions</span></span> 
3. <span data-ttu-id="974c1-114">Сбор параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="974c1-114">Gather configuration settings</span></span> 

<span data-ttu-id="974c1-115">Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, [отправьте запрос в службу поддержки](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="974c1-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="974c1-116">Регистрация приложения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="974c1-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="974c1-117">Приложение необходимо зарегистрировать, даже если вы обращаетесь к API отчетов с помощью сценария.</span><span class="sxs-lookup"><span data-stu-id="974c1-117">You need to register an app even if you are accessing the reporting API using a script.</span></span> <span data-ttu-id="974c1-118">Это позволит получить **идентификатор приложения**, необходимый для вызова авторизации, и ваш код сможет получать маркеры.</span><span class="sxs-lookup"><span data-stu-id="974c1-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code to receive tokens.</span></span>

<span data-ttu-id="974c1-119">Чтобы настроить для каталога доступ к API отчетов Azure AD, необходимо войти на портал Azure с учетной записью администратора Azure, которой также назначена роль участника каталога **глобального администратора** в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="974c1-119">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure portal with an Azure administrator account that is also a member of the **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="974c1-120">В приложениях, работающих под учетными данными с такими административными правами, доступно много возможностей. Поэтому храните в надежном месте идентификатор приложения и секретные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="974c1-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="974c1-121">**Вот как можно зарегистрировать приложение Azure Active Directory.**</span><span class="sxs-lookup"><span data-stu-id="974c1-121">**To register an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="974c1-122">На [портале Azure](https://portal.azure.com) в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="974c1-122">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="974c1-124">В колонке **Azure Active Directory** щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="974c1-124">On the **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="974c1-126">В колонке **Регистрация приложений** на панели инструментов вверху щелкните **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="974c1-126">On the **App registrations** blade, in the toolbar on the top, click **New application registration**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="974c1-128">В колонке **Создание** выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="974c1-128">On the **Create** blade, perform the following steps:</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="974c1-130">а.</span><span class="sxs-lookup"><span data-stu-id="974c1-130">a.</span></span> <span data-ttu-id="974c1-131">В текстовом поле **Имя** введите `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="974c1-131">In the **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="974c1-132">b.</span><span class="sxs-lookup"><span data-stu-id="974c1-132">b.</span></span> <span data-ttu-id="974c1-133">В качестве **типа приложения** выберите **Веб-приложение или API**.</span><span class="sxs-lookup"><span data-stu-id="974c1-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="974c1-134">c.</span><span class="sxs-lookup"><span data-stu-id="974c1-134">c.</span></span> <span data-ttu-id="974c1-135">В текстовом поле **URL-адрес входа** введите `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="974c1-135">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="974c1-136">г)</span><span class="sxs-lookup"><span data-stu-id="974c1-136">d.</span></span> <span data-ttu-id="974c1-137">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="974c1-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="974c1-138">Предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="974c1-138">Grant permissions</span></span> 

<span data-ttu-id="974c1-139">Цель этого этапа — предоставить приложению разрешения **Чтение данных каталога** для API **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="974c1-139">The objective of this step is to grant your application **Read directory data** permissions to the **Windows Azure Active Directory** API.</span></span>

![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="974c1-141">**Вот как можно предоставить приложению разрешения на использование API.**</span><span class="sxs-lookup"><span data-stu-id="974c1-141">**To grant your application permission to use the API:**</span></span>

1. <span data-ttu-id="974c1-142">В колонке **Регистрация приложений** в списке приложений щелкните **Reporting API application** (Приложение API отчетов).</span><span class="sxs-lookup"><span data-stu-id="974c1-142">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="974c1-143">В колонке **Reporting API application** (Приложение API отчетов) на панели инструментов вверху щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="974c1-143">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="974c1-145">В колонке **Параметры** щелкните **Необходимые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="974c1-145">On the **Settings** blade, click **Required permissions**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="974c1-147">В колонке **Необходимые разрешения** в списке **API** щелкните **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="974c1-147">On the **Required permissions** blade, in the **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="974c1-149">В колонке **Включить доступ** выберите **Чтение данных каталога**.</span><span class="sxs-lookup"><span data-stu-id="974c1-149">On the **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="974c1-151">На панели инструментов вверху щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="974c1-151">In the toolbar on the top, click **Save**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="974c1-153">Сбор параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="974c1-153">Gather configuration settings</span></span> 
<span data-ttu-id="974c1-154">В этом разделе показано, как получить из каталога следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="974c1-154">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="974c1-155">Доменное имя</span><span class="sxs-lookup"><span data-stu-id="974c1-155">Domain name</span></span>
* <span data-ttu-id="974c1-156">Идентификатор клиента</span><span class="sxs-lookup"><span data-stu-id="974c1-156">Client ID</span></span>
* <span data-ttu-id="974c1-157">Секрет клиента</span><span class="sxs-lookup"><span data-stu-id="974c1-157">Client secret</span></span>

<span data-ttu-id="974c1-158">Эти значения необходимы при настройке вызовов API отчетов.</span><span class="sxs-lookup"><span data-stu-id="974c1-158">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="974c1-159">Получение имени домена</span><span class="sxs-lookup"><span data-stu-id="974c1-159">Get your domain name</span></span>

<span data-ttu-id="974c1-160">**Вот как можно получить доменное имя.**</span><span class="sxs-lookup"><span data-stu-id="974c1-160">**To get your domain name:**</span></span>

1. <span data-ttu-id="974c1-161">На [портале Azure](https://portal.azure.com) в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="974c1-161">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="974c1-163">В колонке **Azure Active Directory** щелкните **Доменные имена**.</span><span class="sxs-lookup"><span data-stu-id="974c1-163">On the **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="974c1-165">Скопируйте нужное доменное имя из списка доменов.</span><span class="sxs-lookup"><span data-stu-id="974c1-165">Copy your domain name from the list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="974c1-166">Получение идентификатора клиента приложения</span><span class="sxs-lookup"><span data-stu-id="974c1-166">Get your application's client ID</span></span>

<span data-ttu-id="974c1-167">**Вот как можно получить идентификатор клиента приложения.**</span><span class="sxs-lookup"><span data-stu-id="974c1-167">**To get your application's client ID:**</span></span>

1. <span data-ttu-id="974c1-168">На [портале Azure](https://portal.azure.com) в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="974c1-168">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="974c1-170">В колонке **Регистрация приложений** в списке приложений щелкните **Reporting API application** (Приложение API отчетов).</span><span class="sxs-lookup"><span data-stu-id="974c1-170">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="974c1-171">В колонке **Reporting API application** (Приложение API отчетов) рядом с полем **Идентификатор приложения** щелкните **Щелкните, чтобы скопировать**.</span><span class="sxs-lookup"><span data-stu-id="974c1-171">On the **Reporting API application** blade, at the **Application ID**, click **Click to copy**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="974c1-173">Получение секрета клиента приложения</span><span class="sxs-lookup"><span data-stu-id="974c1-173">Get your application's client secret</span></span>
<span data-ttu-id="974c1-174">Чтобы получить секретный ключ клиента приложения, необходимо создать ключ и сохранить его значение при сохранении нового ключа, так как это значение невозможно получить позже.</span><span class="sxs-lookup"><span data-stu-id="974c1-174">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

<span data-ttu-id="974c1-175">**Вот как можно получить секрет клиента приложения.**</span><span class="sxs-lookup"><span data-stu-id="974c1-175">**To get your application's client secret:**</span></span>

1. <span data-ttu-id="974c1-176">На [портале Azure](https://portal.azure.com) в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="974c1-176">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="974c1-178">В колонке **Регистрация приложений** в списке приложений щелкните **Reporting API application** (Приложение API отчетов).</span><span class="sxs-lookup"><span data-stu-id="974c1-178">On the **App registrations** blade, in the apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="974c1-179">В колонке **Reporting API application** (Приложение API отчетов) на панели инструментов вверху щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="974c1-179">On the **Reporting API application** blade, in the toolbar on the top, click **Settings**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="974c1-181">В колонке **Параметры** в разделе **APIR Access** (Доступ APIR) щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="974c1-181">On the **Settings** blade, in the **APIR Access** section, click **Keys**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="974c1-183">В колонке **Ключи** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="974c1-183">On the **Keys** blade, perform the following steps:</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="974c1-185">а.</span><span class="sxs-lookup"><span data-stu-id="974c1-185">a.</span></span> <span data-ttu-id="974c1-186">В текстовом поле **Описание** введите `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="974c1-186">In the **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="974c1-187">b.</span><span class="sxs-lookup"><span data-stu-id="974c1-187">b.</span></span> <span data-ttu-id="974c1-188">Для параметра **Срок действия истекает** выберите значение **Через 2 года**.</span><span class="sxs-lookup"><span data-stu-id="974c1-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="974c1-189">c.</span><span class="sxs-lookup"><span data-stu-id="974c1-189">c.</span></span> <span data-ttu-id="974c1-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="974c1-190">Click **Save**.</span></span>

    <span data-ttu-id="974c1-191">г)</span><span class="sxs-lookup"><span data-stu-id="974c1-191">d.</span></span> <span data-ttu-id="974c1-192">Скопируйте значение ключа.</span><span class="sxs-lookup"><span data-stu-id="974c1-192">Copy the key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="974c1-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="974c1-193">Next Steps</span></span>
* <span data-ttu-id="974c1-194">Хотите получать доступ к данным из API отчетов Azure AD программным образом?</span><span class="sxs-lookup"><span data-stu-id="974c1-194">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="974c1-195">См. статью [Приступая к работе с API отчетов Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="974c1-195">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="974c1-196">Дополнительные сведения об отчетах Azure Active Directory см. в статье [Руководство по отчетам Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="974c1-196">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

