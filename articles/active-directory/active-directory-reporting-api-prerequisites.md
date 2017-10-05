---
title: "Предварительные требования для доступа к API отчетов Azure AD. | Документация Майкрософт"
description: "Узнайте о предварительных требованиях для доступа к API отчетов Azure AD"
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
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="47f38-104">Предварительные требования для доступа к API отчетов Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f38-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="47f38-105">[Интерфейсы API отчетов Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) предоставляют программный доступ к данным с помощью набора интерфейсов API на базе REST.</span><span class="sxs-lookup"><span data-stu-id="47f38-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="47f38-106">Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования.</span><span class="sxs-lookup"><span data-stu-id="47f38-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="47f38-107">API отчетов использует [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) для авторизации доступа к веб-API.</span><span class="sxs-lookup"><span data-stu-id="47f38-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="47f38-108">Чтобы подготовить доступ к API отчетов, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="47f38-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="47f38-109">Создайте приложение в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47f38-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="47f38-110">Предоставьте ему соответствующие разрешения для доступа к данным Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47f38-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="47f38-111">Получите параметры конфигурации из каталога.</span><span class="sxs-lookup"><span data-stu-id="47f38-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="47f38-112">Чтобы задать вопросы, обговорить проблемы или предоставить отзыв, обратитесь в [службу поддержки по инструментам создания отчетов AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="47f38-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="47f38-113">Создание приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f38-113">Create an Azure AD application</span></span>
<span data-ttu-id="47f38-114">Чтобы настроить для каталога доступ к API отчетов Azure AD, необходимо войти на классический портал Azure с помощью учетной записи администратора подписки Azure, которой также назначена роль участника каталога глобального администратора в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47f38-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47f38-115">В приложениях, работающих под учетными данными с такими административными правами, доступно много возможностей. Поэтому храните в надежном месте идентификатор приложения и секретные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="47f38-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="47f38-116">На [классическом портале Azure](https://manage.windowsazure.com)в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47f38-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="47f38-118">Выберите свой каталог в списке каталогов **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="47f38-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="47f38-119">В меню вверху щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="47f38-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="47f38-121">На нижней панели щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="47f38-121">On the bottom bar, click **Add**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="47f38-123">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение, разрабатываемое моей организацией**.</span><span class="sxs-lookup"><span data-stu-id="47f38-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="47f38-125">В диалоговом окне **Расскажите о своем приложении** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="47f38-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="47f38-127">а.</span><span class="sxs-lookup"><span data-stu-id="47f38-127">a.</span></span> <span data-ttu-id="47f38-128">В текстовом поле **Имя** введите имя (например, приложение API отчетов).</span><span class="sxs-lookup"><span data-stu-id="47f38-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="47f38-129">b.</span><span class="sxs-lookup"><span data-stu-id="47f38-129">b.</span></span> <span data-ttu-id="47f38-130">Выберите **Веб-приложение и/или веб-API**.</span><span class="sxs-lookup"><span data-stu-id="47f38-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="47f38-131">c.</span><span class="sxs-lookup"><span data-stu-id="47f38-131">c.</span></span> <span data-ttu-id="47f38-132">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="47f38-132">Click **Next**.</span></span>
7. <span data-ttu-id="47f38-133">В диалоговом окне **Свойства приложения** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="47f38-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="47f38-135">а.</span><span class="sxs-lookup"><span data-stu-id="47f38-135">a.</span></span> <span data-ttu-id="47f38-136">В текстовом поле **URL-адрес входа** введите `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="47f38-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="47f38-137">b.</span><span class="sxs-lookup"><span data-stu-id="47f38-137">b.</span></span> <span data-ttu-id="47f38-138">В текстовом поле **URI кода приложения** введите ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="47f38-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="47f38-139">c.</span><span class="sxs-lookup"><span data-stu-id="47f38-139">c.</span></span> <span data-ttu-id="47f38-140">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="47f38-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="47f38-141">Предоставление приложению разрешения на использование API</span><span class="sxs-lookup"><span data-stu-id="47f38-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="47f38-142">На [классическом портале Azure](https://manage.windowsazure.com/)в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47f38-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="47f38-144">Выберите свой каталог в списке каталогов **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="47f38-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="47f38-145">В меню вверху щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="47f38-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="47f38-147">В списке приложений выберите созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="47f38-147">In the applications list, select your newly created application.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="47f38-149">В верхнем меню щелкните **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="47f38-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="47f38-151">В разделе **Разрешения для других приложений** для ресурса **Azure Active Directory** щелкните раскрывающийся список **Разрешения приложения** и выберите пункт **Прочитать данные каталога**.</span><span class="sxs-lookup"><span data-stu-id="47f38-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="47f38-153">На нижней панели щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="47f38-153">On the bottom bar, click **Save**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="47f38-155">Получите параметры конфигурации из каталога.</span><span class="sxs-lookup"><span data-stu-id="47f38-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="47f38-156">В этом разделе показано, как получить из каталога следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="47f38-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="47f38-157">Доменное имя</span><span class="sxs-lookup"><span data-stu-id="47f38-157">Domain name</span></span>
* <span data-ttu-id="47f38-158">Идентификатор клиента</span><span class="sxs-lookup"><span data-stu-id="47f38-158">Client ID</span></span>
* <span data-ttu-id="47f38-159">Секрет клиента</span><span class="sxs-lookup"><span data-stu-id="47f38-159">Client secret</span></span>

<span data-ttu-id="47f38-160">Эти значения необходимы при настройке вызовов API отчетов.</span><span class="sxs-lookup"><span data-stu-id="47f38-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="47f38-161">Получение имени домена</span><span class="sxs-lookup"><span data-stu-id="47f38-161">Get your domain name</span></span>
1. <span data-ttu-id="47f38-162">На [классическом портале Azure](https://manage.windowsazure.com)в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47f38-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="47f38-164">Выберите свой каталог в списке каталогов **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="47f38-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="47f38-165">В меню вверху щелкните **Домены**.</span><span class="sxs-lookup"><span data-stu-id="47f38-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="47f38-167">Скопируйте имя домена в столбце **Доменное имя** .</span><span class="sxs-lookup"><span data-stu-id="47f38-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="47f38-169">Получение идентификатора клиента приложения</span><span class="sxs-lookup"><span data-stu-id="47f38-169">Get the application's client ID</span></span>
1. <span data-ttu-id="47f38-170">На [классическом портале Azure](https://manage.windowsazure.com)в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47f38-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="47f38-172">Выберите свой каталог в списке каталогов **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="47f38-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="47f38-173">В меню вверху щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="47f38-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="47f38-175">В списке приложений выберите созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="47f38-175">In the applications list, select your newly created application.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="47f38-177">В верхнем меню щелкните **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="47f38-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="47f38-179">Скопируйте значение **идентификатор клиента**.</span><span class="sxs-lookup"><span data-stu-id="47f38-179">Copy your **Client ID**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="47f38-181">Получение секрета клиента приложения</span><span class="sxs-lookup"><span data-stu-id="47f38-181">Get the application's client secret</span></span>
<span data-ttu-id="47f38-182">Чтобы получить секретный ключ клиента приложения, необходимо создать ключ и сохранить его значение при сохранении нового ключа, так как это значение невозможно получить позже.</span><span class="sxs-lookup"><span data-stu-id="47f38-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="47f38-183">На [классическом портале Azure](https://manage.windowsazure.com)в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47f38-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="47f38-185">Выберите свой каталог в списке каталогов **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="47f38-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="47f38-186">В меню вверху щелкните **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="47f38-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="47f38-188">В списке приложений выберите созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="47f38-188">In the applications list, select your newly created application.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="47f38-190">В верхнем меню щелкните **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="47f38-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="47f38-192">В разделе **Ключи** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="47f38-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="47f38-194">а.</span><span class="sxs-lookup"><span data-stu-id="47f38-194">a.</span></span> <span data-ttu-id="47f38-195">В списке значений длительности выберите значение длительности.</span><span class="sxs-lookup"><span data-stu-id="47f38-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="47f38-196">b.</span><span class="sxs-lookup"><span data-stu-id="47f38-196">b.</span></span> <span data-ttu-id="47f38-197">На нижней панели щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="47f38-197">On the bottom bar, click **Save**.</span></span>
   
    ![Регистрация приложения](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="47f38-199">c.</span><span class="sxs-lookup"><span data-stu-id="47f38-199">c.</span></span> <span data-ttu-id="47f38-200">Скопируйте значение ключа.</span><span class="sxs-lookup"><span data-stu-id="47f38-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47f38-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="47f38-201">Next Steps</span></span>
* <span data-ttu-id="47f38-202">Хотите получать доступ к данным из API отчетов Azure AD программным образом?</span><span class="sxs-lookup"><span data-stu-id="47f38-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="47f38-203">См. статью [Приступая к работе с API отчетов Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="47f38-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="47f38-204">Дополнительные сведения об отчетах Azure Active Directory см. в статье [Руководство по отчетам Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="47f38-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

