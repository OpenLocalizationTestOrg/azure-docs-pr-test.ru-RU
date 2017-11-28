---
title: "API отчетов Azure AD hello tooaccess aaaPrerequisites | Документы Microsoft"
description: "Дополнительные сведения об отчетности API hello Azure AD tooaccess hello предварительные требования"
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
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="fb683-103">API отчетов hello Azure AD tooaccess предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fb683-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="fb683-104">Hello [reporting API-интерфейсов Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) предоставить программный доступ к данным toohello через набор API на основе REST.</span><span class="sxs-lookup"><span data-stu-id="fb683-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="fb683-105">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="fb683-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="fb683-106">модуль отчетов API Hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize доступа toohello веб-API.</span><span class="sxs-lookup"><span data-stu-id="fb683-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="fb683-107">tooget доступ toohello данных отчетов с помощью hello API, необходимо toohave одно из следующих ролях, назначенных hello:</span><span class="sxs-lookup"><span data-stu-id="fb683-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="fb683-108">Чтение данных безопасности</span><span class="sxs-lookup"><span data-stu-id="fb683-108">Security Reader</span></span>
- <span data-ttu-id="fb683-109">администратор безопасности;</span><span class="sxs-lookup"><span data-stu-id="fb683-109">Security Admin</span></span>
- <span data-ttu-id="fb683-110">глобальный администратор.</span><span class="sxs-lookup"><span data-stu-id="fb683-110">Global Admin</span></span>


<span data-ttu-id="fb683-111">tooprepare вашей reporting API toohello доступ, необходимо:</span><span class="sxs-lookup"><span data-stu-id="fb683-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="fb683-112">Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="fb683-112">Register an application</span></span> 
2. <span data-ttu-id="fb683-113">предоставьте разрешения;</span><span class="sxs-lookup"><span data-stu-id="fb683-113">Grant permissions</span></span> 
3. <span data-ttu-id="fb683-114">Сбор параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="fb683-114">Gather configuration settings</span></span> 

<span data-ttu-id="fb683-115">Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, [отправьте запрос в службу поддержки](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="fb683-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="fb683-116">Регистрация приложения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb683-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="fb683-117">Необходимо tooregister приложения, даже если вы пользуетесь hello reporting API, с помощью скрипта.</span><span class="sxs-lookup"><span data-stu-id="fb683-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="fb683-118">Этот метод позволяет **идентификатор приложения**, которая используется для вызова авторизации и позволяет маркеры tooreceive кода.</span><span class="sxs-lookup"><span data-stu-id="fb683-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="fb683-119">tooconfigure directory API отчетов tooaccess hello Azure AD, необходимо войти в toohello портал Azure с учетной записью администратора Azure, который также является членом hello **глобального администратора** роли каталога в клиенте Azure AD .</span><span class="sxs-lookup"><span data-stu-id="fb683-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb683-120">Приложениям, выполняемым учетные данные с правами «admin», как это может быть очень мощные, поэтому имейте безопасного убедиться, что tookeep hello идентификатор и секрет учетные данные приложения.</span><span class="sxs-lookup"><span data-stu-id="fb683-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="fb683-121">**tooregister приложение Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="fb683-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="fb683-122">В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb683-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="fb683-124">На hello **Azure Active Directory** колонка, щелкните **регистрации приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb683-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="fb683-126">На hello **регистрации приложения** колонке hello инструментов в верхней части страницы приветствия щелкните **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb683-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="fb683-128">На hello **создать** колонки, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fb683-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="fb683-130">а.</span><span class="sxs-lookup"><span data-stu-id="fb683-130">a.</span></span> <span data-ttu-id="fb683-131">В hello **имя** введите `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="fb683-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="fb683-132">b.</span><span class="sxs-lookup"><span data-stu-id="fb683-132">b.</span></span> <span data-ttu-id="fb683-133">В качестве **типа приложения** выберите **Веб-приложение или API**.</span><span class="sxs-lookup"><span data-stu-id="fb683-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="fb683-134">c.</span><span class="sxs-lookup"><span data-stu-id="fb683-134">c.</span></span> <span data-ttu-id="fb683-135">В hello **URL-адрес входа** введите `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="fb683-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="fb683-136">d.</span><span class="sxs-lookup"><span data-stu-id="fb683-136">d.</span></span> <span data-ttu-id="fb683-137">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fb683-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="fb683-138">Предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="fb683-138">Grant permissions</span></span> 

<span data-ttu-id="fb683-139">Цель этого шага Hello является toogrant приложения **читать данные каталога** toohello разрешения **Windows Azure Active Directory** API.</span><span class="sxs-lookup"><span data-stu-id="fb683-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="fb683-141">**toogrant вашего приложения hello toouse разрешение API:**</span><span class="sxs-lookup"><span data-stu-id="fb683-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="fb683-142">На hello **регистрации приложения** колонки в списке приложений hello щелкните **Reporting API приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb683-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="fb683-143">На hello **Reporting API приложения** колонке hello инструментов в верхней части страницы приветствия щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="fb683-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="fb683-145">На hello **параметры** колонка, щелкните **требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="fb683-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="fb683-147">На hello **разрешения, необходимые** колонки в hello **API** выберите **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb683-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="fb683-149">На hello **включить доступ** колонке выберите **читать данные каталога**.</span><span class="sxs-lookup"><span data-stu-id="fb683-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="fb683-151">Щелкните hello панели инструментов в верхней части hello **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb683-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="fb683-153">Сбор параметров конфигурации</span><span class="sxs-lookup"><span data-stu-id="fb683-153">Gather configuration settings</span></span> 
<span data-ttu-id="fb683-154">В этом разделе показано, как hello tooget следующие параметры из каталога:</span><span class="sxs-lookup"><span data-stu-id="fb683-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="fb683-155">Доменное имя</span><span class="sxs-lookup"><span data-stu-id="fb683-155">Domain name</span></span>
* <span data-ttu-id="fb683-156">Идентификатор клиента</span><span class="sxs-lookup"><span data-stu-id="fb683-156">Client ID</span></span>
* <span data-ttu-id="fb683-157">Секрет клиента</span><span class="sxs-lookup"><span data-stu-id="fb683-157">Client secret</span></span>

<span data-ttu-id="fb683-158">Эти значения необходимо при настройке отчетов API toohello вызовов.</span><span class="sxs-lookup"><span data-stu-id="fb683-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="fb683-159">Получение имени домена</span><span class="sxs-lookup"><span data-stu-id="fb683-159">Get your domain name</span></span>

<span data-ttu-id="fb683-160">**tooget доменного имени:**</span><span class="sxs-lookup"><span data-stu-id="fb683-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="fb683-161">В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb683-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="fb683-163">На hello **Azure Active Directory** колонка, щелкните **доменных имен**.</span><span class="sxs-lookup"><span data-stu-id="fb683-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="fb683-165">Скопируйте имя домена из списка доменов hello.</span><span class="sxs-lookup"><span data-stu-id="fb683-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="fb683-166">Получение идентификатора клиента приложения</span><span class="sxs-lookup"><span data-stu-id="fb683-166">Get your application's client ID</span></span>

<span data-ttu-id="fb683-167">**tooget идентификатор клиента приложения:**</span><span class="sxs-lookup"><span data-stu-id="fb683-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="fb683-168">В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb683-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="fb683-170">На hello **регистрации приложения** колонки в списке приложений hello щелкните **Reporting API приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb683-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="fb683-171">На hello **Reporting API приложения** колонки в hello **идентификатор приложения**, нажмите кнопку **щелкните toocopy**.</span><span class="sxs-lookup"><span data-stu-id="fb683-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="fb683-173">Получение секрета клиента приложения</span><span class="sxs-lookup"><span data-stu-id="fb683-173">Get your application's client secret</span></span>
<span data-ttu-id="fb683-174">tooget клиентского приложения в тайне, нужно toocreate новый ключ и сохранить его значение при сохранении hello новый ключ, так как он не возможные tooretrieve позже больше это значение.</span><span class="sxs-lookup"><span data-stu-id="fb683-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="fb683-175">**tooget секрет клиента приложения:**</span><span class="sxs-lookup"><span data-stu-id="fb683-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="fb683-176">В hello [портал Azure](https://portal.azure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fb683-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="fb683-178">На hello **регистрации приложения** колонки в списке приложений hello щелкните **Reporting API приложения**.</span><span class="sxs-lookup"><span data-stu-id="fb683-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="fb683-179">На hello **Reporting API приложения** колонке hello инструментов в верхней части страницы приветствия щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="fb683-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="fb683-181">На hello **параметры** колонки в hello **доступа APIR** щелкните **ключей**.</span><span class="sxs-lookup"><span data-stu-id="fb683-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="fb683-183">На hello **ключей** колонки, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="fb683-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="fb683-185">а.</span><span class="sxs-lookup"><span data-stu-id="fb683-185">a.</span></span> <span data-ttu-id="fb683-186">В hello **описание** введите `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="fb683-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="fb683-187">b.</span><span class="sxs-lookup"><span data-stu-id="fb683-187">b.</span></span> <span data-ttu-id="fb683-188">Для параметра **Срок действия истекает** выберите значение **Через 2 года**.</span><span class="sxs-lookup"><span data-stu-id="fb683-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="fb683-189">c.</span><span class="sxs-lookup"><span data-stu-id="fb683-189">c.</span></span> <span data-ttu-id="fb683-190">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fb683-190">Click **Save**.</span></span>

    <span data-ttu-id="fb683-191">d.</span><span class="sxs-lookup"><span data-stu-id="fb683-191">d.</span></span> <span data-ttu-id="fb683-192">Скопируйте значение ключа hello.</span><span class="sxs-lookup"><span data-stu-id="fb683-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fb683-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb683-193">Next Steps</span></span>
* <span data-ttu-id="fb683-194">Бы вы, как данные из Azure AD hello hello tooaccess reporting API программным способом</span><span class="sxs-lookup"><span data-stu-id="fb683-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="fb683-195">Извлечение [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb683-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="fb683-196">Если вы хотите toofind дополнительных сведений об отчетах Azure Active Directory, см. раздел hello [Azure Active Directory руководство по отчетам](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="fb683-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

