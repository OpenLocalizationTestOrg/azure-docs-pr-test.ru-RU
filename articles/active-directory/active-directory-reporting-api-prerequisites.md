---
title: "aaaPrerequisites tooaccess hello Azure AD отчетов API. | Документация Майкрософт"
description: "Дополнительные сведения об отчетности API hello Azure AD tooaccess hello предварительные требования"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="41c57-104">API отчетов hello Azure AD tooaccess предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41c57-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="41c57-105">Hello [reporting API-интерфейсов Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) предоставить программный доступ к данным toohello через набор API на основе REST.</span><span class="sxs-lookup"><span data-stu-id="41c57-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="41c57-106">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="41c57-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="41c57-107">модуль отчетов API Hello [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize доступа toohello веб-API.</span><span class="sxs-lookup"><span data-stu-id="41c57-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="41c57-108">tooprepare вашей reporting API toohello доступ, необходимо:</span><span class="sxs-lookup"><span data-stu-id="41c57-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="41c57-109">Создайте приложение в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41c57-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="41c57-110">Приложения соответствующие разрешения GRANT hello tooaccess hello данных Azure AD</span><span class="sxs-lookup"><span data-stu-id="41c57-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="41c57-111">Получите параметры конфигурации из каталога.</span><span class="sxs-lookup"><span data-stu-id="41c57-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="41c57-112">Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, обратитесь в [службу поддержки по инструментам создания отчетов AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="41c57-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="41c57-113">Создание приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="41c57-113">Create an Azure AD application</span></span>
<span data-ttu-id="41c57-114">tooconfigure directory API отчетов tooaccess hello Azure AD, необходимо войти в toohello классический портал Azure с учетной записью администратора подписки Azure, который также является членом роли каталога hello глобального администратора в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41c57-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41c57-115">Приложениям, выполняемым учетные данные с правами «admin», как это может быть очень мощные, поэтому имейте безопасного убедиться, что tookeep hello идентификатор и секрет учетные данные приложения.</span><span class="sxs-lookup"><span data-stu-id="41c57-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="41c57-116">В hello [классический портал Azure](https://manage.windowsazure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41c57-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="41c57-118">Из hello **active directory** список, выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="41c57-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="41c57-119">В меню в верхней части hello hello выберите **приложений**.</span><span class="sxs-lookup"><span data-stu-id="41c57-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="41c57-121">На нижней панели hello щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="41c57-121">On hello bottom bar, click **Add**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="41c57-123">На hello **что вам требуется toodo?** диалоговое окно, нажмите кнопку **добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="41c57-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="41c57-125">На hello **Расскажите о своем приложении** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="41c57-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="41c57-127">а.</span><span class="sxs-lookup"><span data-stu-id="41c57-127">a.</span></span> <span data-ttu-id="41c57-128">В hello **имя** текстовом поле введите имя (например: приложения API для отчетов).</span><span class="sxs-lookup"><span data-stu-id="41c57-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="41c57-129">b.</span><span class="sxs-lookup"><span data-stu-id="41c57-129">b.</span></span> <span data-ttu-id="41c57-130">Выберите **Веб-приложение и/или веб-API**.</span><span class="sxs-lookup"><span data-stu-id="41c57-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="41c57-131">c.</span><span class="sxs-lookup"><span data-stu-id="41c57-131">c.</span></span> <span data-ttu-id="41c57-132">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="41c57-132">Click **Next**.</span></span>
7. <span data-ttu-id="41c57-133">На hello **свойства приложения** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="41c57-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="41c57-135">а.</span><span class="sxs-lookup"><span data-stu-id="41c57-135">a.</span></span> <span data-ttu-id="41c57-136">В hello **URL-адрес входа** введите `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="41c57-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="41c57-137">b.</span><span class="sxs-lookup"><span data-stu-id="41c57-137">b.</span></span> <span data-ttu-id="41c57-138">В hello **URI идентификатора приложения** введите ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="41c57-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="41c57-139">c.</span><span class="sxs-lookup"><span data-stu-id="41c57-139">c.</span></span> <span data-ttu-id="41c57-140">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="41c57-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="41c57-141">Предоставьте разрешение hello toouse API вашего приложения</span><span class="sxs-lookup"><span data-stu-id="41c57-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="41c57-142">В hello [классический портал Azure](https://manage.windowsazure.com/), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41c57-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="41c57-144">Из hello **active directory** список, выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="41c57-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="41c57-145">В меню в верхней части hello hello выберите **приложений**.</span><span class="sxs-lookup"><span data-stu-id="41c57-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="41c57-147">В списке приложений hello выберите только что созданный приложения.</span><span class="sxs-lookup"><span data-stu-id="41c57-147">In hello applications list, select your newly created application.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="41c57-149">В меню в верхней части hello hello выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="41c57-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="41c57-151">В hello **tooother разрешения приложений** раздел для hello **Azure Active Directory** ресурсов, щелкните hello **разрешения приложения** раскрывающегося списка, а затем Выберите **читать данные каталога**.</span><span class="sxs-lookup"><span data-stu-id="41c57-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="41c57-153">На нижней панели hello щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="41c57-153">On hello bottom bar, click **Save**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="41c57-155">Получите параметры конфигурации из каталога.</span><span class="sxs-lookup"><span data-stu-id="41c57-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="41c57-156">В этом разделе показано, как hello tooget следующие параметры из каталога:</span><span class="sxs-lookup"><span data-stu-id="41c57-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="41c57-157">Доменное имя</span><span class="sxs-lookup"><span data-stu-id="41c57-157">Domain name</span></span>
* <span data-ttu-id="41c57-158">Идентификатор клиента</span><span class="sxs-lookup"><span data-stu-id="41c57-158">Client ID</span></span>
* <span data-ttu-id="41c57-159">Секрет клиента</span><span class="sxs-lookup"><span data-stu-id="41c57-159">Client secret</span></span>

<span data-ttu-id="41c57-160">Эти значения необходимо при настройке отчетов API toohello вызовов.</span><span class="sxs-lookup"><span data-stu-id="41c57-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="41c57-161">Получение имени домена</span><span class="sxs-lookup"><span data-stu-id="41c57-161">Get your domain name</span></span>
1. <span data-ttu-id="41c57-162">В hello [классический портал Azure](https://manage.windowsazure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41c57-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="41c57-164">Из hello **active directory** список, выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="41c57-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="41c57-165">В меню в верхней части hello hello выберите **домены**.</span><span class="sxs-lookup"><span data-stu-id="41c57-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="41c57-167">В hello **доменное имя** столбца, скопируйте имя домена.</span><span class="sxs-lookup"><span data-stu-id="41c57-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="41c57-169">Получить идентификатор клиента приложения hello</span><span class="sxs-lookup"><span data-stu-id="41c57-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="41c57-170">В hello [классический портал Azure](https://manage.windowsazure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41c57-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="41c57-172">Из hello **active directory** список, выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="41c57-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="41c57-173">В меню в верхней части hello hello выберите **приложений**.</span><span class="sxs-lookup"><span data-stu-id="41c57-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="41c57-175">В списке приложений hello выберите только что созданный приложения.</span><span class="sxs-lookup"><span data-stu-id="41c57-175">In hello applications list, select your newly created application.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="41c57-177">В меню в верхней части hello hello выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="41c57-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="41c57-179">Скопируйте значение **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="41c57-179">Copy your **Client ID**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="41c57-181">Получить секрет клиента приложения hello</span><span class="sxs-lookup"><span data-stu-id="41c57-181">Get hello application's client secret</span></span>
<span data-ttu-id="41c57-182">tooget клиентского приложения в тайне, нужно toocreate новый ключ и сохранить его значение при сохранении hello новый ключ, так как он не возможные tooretrieve позже больше это значение.</span><span class="sxs-lookup"><span data-stu-id="41c57-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="41c57-183">В hello [классический портал Azure](https://manage.windowsazure.com), на левой панели навигации hello, нажмите кнопку **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41c57-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="41c57-185">Из hello **active directory** список, выберите свой каталог.</span><span class="sxs-lookup"><span data-stu-id="41c57-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="41c57-186">В меню в верхней части hello hello выберите **приложений**.</span><span class="sxs-lookup"><span data-stu-id="41c57-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="41c57-188">В списке приложений hello выберите только что созданный приложения.</span><span class="sxs-lookup"><span data-stu-id="41c57-188">In hello applications list, select your newly created application.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="41c57-190">В меню в верхней части hello hello выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="41c57-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="41c57-192">В hello **ключей** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="41c57-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="41c57-194">а.</span><span class="sxs-lookup"><span data-stu-id="41c57-194">a.</span></span> <span data-ttu-id="41c57-195">Выберите из списка длительность hello длительность</span><span class="sxs-lookup"><span data-stu-id="41c57-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="41c57-196">b.</span><span class="sxs-lookup"><span data-stu-id="41c57-196">b.</span></span> <span data-ttu-id="41c57-197">На нижней панели hello щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="41c57-197">On hello bottom bar, click **Save**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="41c57-199">c.</span><span class="sxs-lookup"><span data-stu-id="41c57-199">c.</span></span> <span data-ttu-id="41c57-200">Скопируйте значение ключа hello.</span><span class="sxs-lookup"><span data-stu-id="41c57-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41c57-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41c57-201">Next Steps</span></span>
* <span data-ttu-id="41c57-202">Бы вы, как данные из Azure AD hello hello tooaccess reporting API программным способом</span><span class="sxs-lookup"><span data-stu-id="41c57-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="41c57-203">Извлечение [Приступая к работе с Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="41c57-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="41c57-204">Если вы хотите toofind дополнительных сведений об отчетах Azure Active Directory, см. раздел hello [Azure Active Directory руководство по отчетам](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="41c57-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

