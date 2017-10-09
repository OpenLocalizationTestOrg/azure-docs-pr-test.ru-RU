---
title: "Источник aaaOpen технологии часто задаваемые вопросы про Azure веб-приложений | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о технологиях открытым исходным кодом в веб-приложения hello функция службы приложений Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="42e6e-103">Часто задаваемые вопросы о технологиях с открытым кодом в веб-приложениях Azure</span><span class="sxs-lookup"><span data-stu-id="42e6e-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="42e6e-104">Данная статья содержит ответы toofrequently, задаваемые вопросы (FAQ) о проблемах, связанных с открытым исходным кодом технологии для hello [веб-приложений функции службы приложений Azure](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="42e6e-105">База данных ClearDB не работает.</span><span class="sxs-lookup"><span data-stu-id="42e6e-105">My ClearDB database is down.</span></span> <span data-ttu-id="42e6e-106">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="42e6e-106">How do I resolve this?</span></span>

<span data-ttu-id="42e6e-107">По вопросам, связанным с базами данных, обращайтесь в [службу поддержки ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="42e6e-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="42e6e-108">Ответы toocommon ответы на вопросы о ClearDB см [ClearDB часто задаваемые вопросы о](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="42e6e-109">Почему Моя база данных ClearDB отсутствует в портале hello</span><span class="sxs-lookup"><span data-stu-id="42e6e-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="42e6e-110">Если создать базу данных ClearDB в hello [портал Azure](http://portal.azure.com/), hello базы данных не отображается в hello [классический портал Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="42e6e-111">toowork этой может вручную связать веб-приложения toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="42e6e-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="42e6e-112">Аналогично Если создать базу данных ClearDB в hello [классический портал Azure](http://manage.windowsazure.com/), вы не увидите базу данных в hello [портал Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="42e6e-113">Для этой ситуации нет решения.</span><span class="sxs-lookup"><span data-stu-id="42e6e-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="42e6e-114">Дополнительные сведения см. в статье [Часто задаваемые вопросы о базах данных ClearDB MySql в службе приложений Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="42e6e-115">Почему не удалось перенести базу данных ClearDB при переносе подписки?</span><span class="sxs-lookup"><span data-stu-id="42e6e-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="42e6e-116">При переносе ресурсов из одной подписки в другую действуют некоторые ограничения.</span><span class="sxs-lookup"><span data-stu-id="42e6e-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="42e6e-117">База данных ClearDB MySQL — это сторонняя служба, и она не перемещается при переносе подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="42e6e-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="42e6e-118">Если вы не управляете hello миграции базы данных MySQL, прежде чем переносить ресурсы Azure, базу данных ClearDB MySQL могут быть недоступны.</span><span class="sxs-lookup"><span data-stu-id="42e6e-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="42e6e-119">tooavoid этого, во-первых, вручную перенести базу данных ClearDB, а затем перенести hello подписки Azure для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="42e6e-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="42e6e-120">Дополнительные сведения см. в статье [Часто задаваемые вопросы о базах данных ClearDB MySql в службе приложений Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="42e6e-121">Как включить ведение журнала tootroubleshoot PHP проблемы PHP?</span><span class="sxs-lookup"><span data-stu-id="42e6e-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="42e6e-122">tooturn PHP ведения журнала:</span><span class="sxs-lookup"><span data-stu-id="42e6e-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="42e6e-123">Войдите в tooyour [Kudu веб-сайт](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="42e6e-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="42e6e-124">В верхнем меню hello, выберите **консоли отладки** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="42e6e-125">Выберите hello **сайта** папки.</span><span class="sxs-lookup"><span data-stu-id="42e6e-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="42e6e-126">Выберите hello **wwwroot** папки.</span><span class="sxs-lookup"><span data-stu-id="42e6e-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="42e6e-127">Выберите hello  **+**  значок, а затем выберите **новый файл**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="42e6e-128">Задайте имя файла hello слишком**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="42e6e-129">Выберите значок карандаша hello Далее слишком**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="42e6e-130">Добавьте следующий код в файл hello:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="42e6e-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="42e6e-131">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-131">Select **Save**.</span></span>
10. <span data-ttu-id="42e6e-132">Выберите значок карандаша hello Далее слишком**wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="42e6e-133">Изменить toohello текста hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="42e6e-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="42e6e-134">В hello портал Azure, в меню приложения веб-hello перезапустите веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="42e6e-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="42e6e-135">Дополнительные сведения см. в записи блога [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Включение журналов ошибок WordPress).</span><span class="sxs-lookup"><span data-stu-id="42e6e-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="42e6e-136">Как включить ведение журнала ошибок в приложениях Python, размещенных в службе приложений?</span><span class="sxs-lookup"><span data-stu-id="42e6e-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="42e6e-137">ошибки приложения Python toocapture:</span><span class="sxs-lookup"><span data-stu-id="42e6e-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="42e6e-138">В hello портал Azure, в веб-приложения выберите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="42e6e-139">На hello **параметры** выберите **параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="42e6e-140">В разделе **параметры приложения**, введите hello следующая пара ключ значение:</span><span class="sxs-lookup"><span data-stu-id="42e6e-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="42e6e-141">Ключ: WSGI_LOG.</span><span class="sxs-lookup"><span data-stu-id="42e6e-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="42e6e-142">Значение: D:\home\site\wwwroot\logs.txt (введите собственное имя файла).</span><span class="sxs-lookup"><span data-stu-id="42e6e-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="42e6e-143">Теперь вы увидите ошибки в файле logs.txt hello в папке wwwroot hello.</span><span class="sxs-lookup"><span data-stu-id="42e6e-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="42e6e-144">Как изменить версию hello hello Node.js приложений, размещенных в службе приложений?</span><span class="sxs-lookup"><span data-stu-id="42e6e-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="42e6e-145">версии hello toochange hello Node.js приложения, можно использовать один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="42e6e-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="42e6e-146">В hello портал Azure, используйте **параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="42e6e-147">В hello портал Azure перейдите tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="42e6e-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="42e6e-148">На hello **параметры** колонке выберите **параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="42e6e-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="42e6e-149">В **параметры приложения**, можно включить WEBSITE_NODE_DEFAULT_VERSION как ключ hello и hello версии Node.js необходимо в качестве значения hello.</span><span class="sxs-lookup"><span data-stu-id="42e6e-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="42e6e-150">Go tooyour [Kudu консоли](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="42e6e-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="42e6e-151">toocheck Здравствуйте Node.js версии, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="42e6e-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="42e6e-152">Измените файл iisnode.yml hello.</span><span class="sxs-lookup"><span data-stu-id="42e6e-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="42e6e-153">Изменение версии hello Node.js в файле iisnode.yml hello только задает hello среды выполнения, iisnode использует.</span><span class="sxs-lookup"><span data-stu-id="42e6e-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="42e6e-154">Ваш Kudu cmd, а другие — по-прежнему использовать hello Node.js версии, который задан в **параметры приложения** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="42e6e-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="42e6e-155">tooset hello iisnode.yml вручную, создайте файл iisnode.yml в корневой папке приложения.</span><span class="sxs-lookup"><span data-stu-id="42e6e-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="42e6e-156">В файле hello включите hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="42e6e-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="42e6e-157">Задать hello iisnode.yml файла с помощью package.json во время развертывания исходного элемента управления.</span><span class="sxs-lookup"><span data-stu-id="42e6e-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="42e6e-158">Hello процесс развертывания управления Azure источника включает в себя hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="42e6e-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="42e6e-159">Перемещение содержимого toohello веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="42e6e-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="42e6e-160">Создает скрипт развертывания по умолчанию, если его нет (deploy.cmd, .deployment файлы) в hello веб-приложения корневой папке.</span><span class="sxs-lookup"><span data-stu-id="42e6e-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="42e6e-161">Запускает скрипт развертывания, в котором создается файл iisnode.yml Если упоминается hello Node.js версии в файле package.json hello > ядра`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="42e6e-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="42e6e-162">файл iisnode.yml Hello имеет hello, следующей строкой кода:</span><span class="sxs-lookup"><span data-stu-id="42e6e-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="42e6e-163">Я вижу приветственное сообщение «Ошибка при установке подключения к базе данных» в моем приложении WordPress, размещенного в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="42e6e-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="42e6e-164">Как устранить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="42e6e-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="42e6e-165">Если вы видите эту ошибку в Azure WordPress приложения, tooenable php_errors.log и debug.log, полный hello шаги подробно описаны в [WordPress, включить журналы ошибок](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="42e6e-166">При включении журналы hello воспроизвести ошибки hello и проверьте hello журналы toosee при запуске из подключений:</span><span class="sxs-lookup"><span data-stu-id="42e6e-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="42e6e-167">При появлении этой ошибки в файлах debug.log или php_errors.log приложения превышает hello число подключений.</span><span class="sxs-lookup"><span data-stu-id="42e6e-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="42e6e-168">Если вы размещаете на ClearDB, проверьте hello число подключений, доступных в вашей [план обслуживания](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="42e6e-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="42e6e-169">Как отлаживать приложение Node.js, размещенное в службе приложений?</span><span class="sxs-lookup"><span data-stu-id="42e6e-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="42e6e-170">Go tooyour [Kudu консоли](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="42e6e-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="42e6e-171">Папка logs приложения перейдите tooyour (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="42e6e-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="42e6e-172">В файле logging_errors.txt hello проверьте содержимое.</span><span class="sxs-lookup"><span data-stu-id="42e6e-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="42e6e-173">Как установить собственные модули Python в веб-приложении службы приложений или приложении API?</span><span class="sxs-lookup"><span data-stu-id="42e6e-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="42e6e-174">Некоторые пакеты невозможно установить с помощью pip в Azure.</span><span class="sxs-lookup"><span data-stu-id="42e6e-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="42e6e-175">Hello пакета могут быть недоступны на hello индекс пакета Python или компилятор может потребоваться (компилятора недоступен на компьютере hello, на котором выполняется веб-приложение hello в службе приложений).</span><span class="sxs-lookup"><span data-stu-id="42e6e-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="42e6e-176">Сведения об установке собственных модулей в веб-приложениях службы приложений или приложениях API см. в [этой записи блога](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="42e6e-177">Развертывание Django приложение tooApp службы с помощью Git и hello новой версии Python</span><span class="sxs-lookup"><span data-stu-id="42e6e-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="42e6e-178">Сведения об установке Django см. в разделе [развертывание Django приложение tooApp службы](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="42e6e-179">Где находятся файлы журналов Tomcat hello, расположенные?</span><span class="sxs-lookup"><span data-stu-id="42e6e-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="42e6e-180">Для развертываний Microsoft Azure Marketplace и пользовательских развертываний:</span><span class="sxs-lookup"><span data-stu-id="42e6e-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="42e6e-181">Расположение папки: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs.</span><span class="sxs-lookup"><span data-stu-id="42e6e-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="42e6e-182">Необходимые файлы:</span><span class="sxs-lookup"><span data-stu-id="42e6e-182">Files of interest:</span></span>
    * <span data-ttu-id="42e6e-183">catalina.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="42e6e-184">host-manager.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="42e6e-185">localhost.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="42e6e-186">manager.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="42e6e-187">site_access_log.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="42e6e-188">Для развертываний из меню **Параметры приложения** портала:</span><span class="sxs-lookup"><span data-stu-id="42e6e-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="42e6e-189">Расположение папки: D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="42e6e-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="42e6e-190">Необходимые файлы:</span><span class="sxs-lookup"><span data-stu-id="42e6e-190">Files of interest:</span></span>
    * <span data-ttu-id="42e6e-191">catalina.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="42e6e-192">host-manager.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="42e6e-193">localhost.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="42e6e-194">manager.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="42e6e-195">site_access_log.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="42e6e-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="42e6e-196">Как устранить ошибки подключения драйвера JDBC Driver?</span><span class="sxs-lookup"><span data-stu-id="42e6e-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="42e6e-197">Может появиться следующие сообщения в журналах Tomcat hello:</span><span class="sxs-lookup"><span data-stu-id="42e6e-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="42e6e-198">Ошибка hello tooresolve:</span><span class="sxs-lookup"><span data-stu-id="42e6e-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="42e6e-199">Удалите файл sqljdbc*.jar hello из папки приложения/lib.</span><span class="sxs-lookup"><span data-stu-id="42e6e-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="42e6e-200">Если вы используете hello пользовательского Tomcat или Azure Marketplace Tomcat веб-сервера, скопируйте эту папку lib файл toohello .jar Tomcat.</span><span class="sxs-lookup"><span data-stu-id="42e6e-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="42e6e-201">При включении Java из hello портал Azure (выберите **Java 1.8** > **сервера Tomcat**), копия sqljdbc.* hello jar-файл в папке hello, tooyour параллельные приложения.</span><span class="sxs-lookup"><span data-stu-id="42e6e-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="42e6e-202">Затем добавьте следующие файл web.config toohello параметр classpath hello:</span><span class="sxs-lookup"><span data-stu-id="42e6e-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="42e6e-203">Почему возникают ошибки при попытке toocopy файлы журнала в режиме реального времени?</span><span class="sxs-lookup"><span data-stu-id="42e6e-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="42e6e-204">При попытке toocopy динамической журнала файлов для приложения Java (например, Tomcat), может отображаться следующая ошибка FTP:</span><span class="sxs-lookup"><span data-stu-id="42e6e-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="42e6e-205">сообщение об ошибке Hello может зависеть от клиента hello FTP.</span><span class="sxs-lookup"><span data-stu-id="42e6e-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="42e6e-206">Все приложения Java имеют эту проблему.</span><span class="sxs-lookup"><span data-stu-id="42e6e-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="42e6e-207">Только Kudu поддерживает загрузку этого файла во время выполнения приложение hello.</span><span class="sxs-lookup"><span data-stu-id="42e6e-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="42e6e-208">Остановка приложение hello позволяет доступа по FTP toothese файлов.</span><span class="sxs-lookup"><span data-stu-id="42e6e-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="42e6e-209">Другое решение — toowrite веб-задания, который выполняется по расписанию и копирует эти файлы tooa другой каталог.</span><span class="sxs-lookup"><span data-stu-id="42e6e-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="42e6e-210">Пример проекта, в разделе hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) проекта.</span><span class="sxs-lookup"><span data-stu-id="42e6e-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="42e6e-211">Расположение файлов журнала hello для Jetty</span><span class="sxs-lookup"><span data-stu-id="42e6e-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="42e6e-212">Marketplace и развертывание пользовательских hello файл журнала находится в папке D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello.</span><span class="sxs-lookup"><span data-stu-id="42e6e-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="42e6e-213">Обратите внимание, что расположение папки hello зависит от версии hello Jetty, вы используете.</span><span class="sxs-lookup"><span data-stu-id="42e6e-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="42e6e-214">Например путь hello предназначена для Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="42e6e-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="42e6e-215">Найдите файл jetty_*ГГГГ_ММ_ДД*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="42e6e-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="42e6e-216">Для развертываний портала параметр приложения hello файл журнала находится в D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="42e6e-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="42e6e-217">Найдите файл jetty_*ГГГГ_ММ_ДД*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="42e6e-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="42e6e-218">Можно ли отправлять электронные сообщения из веб-приложения Azure?</span><span class="sxs-lookup"><span data-stu-id="42e6e-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="42e6e-219">Служба приложений не имеет встроенной функции отправки электронных сообщений.</span><span class="sxs-lookup"><span data-stu-id="42e6e-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="42e6e-220">Альтернативные варианты отправки электронных сообщений из приложения см. в [этом обсуждении Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="42e6e-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="42e6e-221">Почему моего сайта WordPress перенаправления tooanother URL-адрес?</span><span class="sxs-lookup"><span data-stu-id="42e6e-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="42e6e-222">Если вы недавно перенесли tooAzure WordPress может перенаправить toohello старые URL-адрес домена.</span><span class="sxs-lookup"><span data-stu-id="42e6e-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="42e6e-223">Это вызвано параметр базы данных MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="42e6e-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="42e6e-224">WordPress контактному лицу + — это расширение узла Azure, можно использовать URL-адрес перенаправления hello tooupdate непосредственно в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="42e6e-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="42e6e-225">Дополнительные сведения об использовании WordPress Buddy+ см. в записи блога [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Средства WordPress и перенос базы данных MySQL с помощью WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="42e6e-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="42e6e-226">Кроме того, при желании URL-адреса перенаправления hello toomanually обновления с помощью SQL-запросы или PHPMyAdmin см [WordPress: перенаправление URL-адрес toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="42e6e-227">Как изменить пароль для входа в WordPress?</span><span class="sxs-lookup"><span data-stu-id="42e6e-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="42e6e-228">Если вы забыли пароль входа в WordPress, можно использовать WordPress контактному лицу + tooupdate его.</span><span class="sxs-lookup"><span data-stu-id="42e6e-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="42e6e-229">ваш пароль, hello установки WordPress контактному лицу + Azure расширение сайта последующем выполнении hello шаги описаны в tooreset [WordPress средства и миграции MySQL WordPress контактному лицу +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="42e6e-230">Не удается выполнить вход tooWordPress</span><span class="sxs-lookup"><span data-stu-id="42e6e-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="42e6e-231">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="42e6e-231">How do I resolve this?</span></span>

<span data-ttu-id="42e6e-232">Если вы не можете войти в WordPress после установки подключаемого модуля, возможно, вы установили не тот модуль.</span><span class="sxs-lookup"><span data-stu-id="42e6e-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="42e6e-233">WordPress Buddy+ — это расширение сайта Azure, с помощью которого можно отключить подключаемые модули в WordPress.</span><span class="sxs-lookup"><span data-stu-id="42e6e-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="42e6e-234">Дополнительные сведения см. в записи блога [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Средства WordPress и перенос базы данных MySQL с помощью WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="42e6e-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="42e6e-235">Как перенести базу данных WordPress?</span><span class="sxs-lookup"><span data-stu-id="42e6e-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="42e6e-236">У вас есть несколько вариантов для миграции базы данных MySQL hello, веб-сайт WordPress подключенных tooyour:</span><span class="sxs-lookup"><span data-stu-id="42e6e-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="42e6e-237">Разработчики: Используйте hello [командной строки или PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="42e6e-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="42e6e-238">с помощью [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (остальные пользователи).</span><span class="sxs-lookup"><span data-stu-id="42e6e-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="42e6e-239">Как повысить уровень защиты WordPress?</span><span class="sxs-lookup"><span data-stu-id="42e6e-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="42e6e-240">toolearn о рекомендациях по безопасности для WordPress, в разделе [советы и рекомендации по обеспечению безопасности WordPress Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="42e6e-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="42e6e-241">Удается toouse PHPMyAdmin и hello сообщение «Доступ запрещен».</span><span class="sxs-lookup"><span data-stu-id="42e6e-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="42e6e-242">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="42e6e-242">How do I resolve this?</span></span>

<span data-ttu-id="42e6e-243">Данная проблема возникает, если в приложении функции hello MySQL еще не запущена в данном экземпляре службы приложений.</span><span class="sxs-lookup"><span data-stu-id="42e6e-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="42e6e-244">tooresolve hello проблему, попробуйте tooaccess веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="42e6e-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="42e6e-245">При этом запустится hello необходимых процессов, включая процесс hello MySQL в приложении.</span><span class="sxs-lookup"><span data-stu-id="42e6e-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="42e6e-246">tooverify с MySQL, выполняется в приложении в обозреватель процессов, убедитесь, что mysqld.exe указывается в процессах hello.</span><span class="sxs-lookup"><span data-stu-id="42e6e-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="42e6e-247">Убедившись, что MySQL в приложении работает, попробуйте toouse PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="42e6e-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="42e6e-248">Произошла ошибка HTTP 403 при экспорте базы данных MySQL в приложении с помощью PHPMyadmin или повторите tooimport.</span><span class="sxs-lookup"><span data-stu-id="42e6e-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="42e6e-249">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="42e6e-249">How do I resolve this?</span></span>

<span data-ttu-id="42e6e-250">Это известная ошибка в старой версии браузера Chrome.</span><span class="sxs-lookup"><span data-stu-id="42e6e-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="42e6e-251">проблема tooresolve hello, новая версия обновления tooa Chrome.</span><span class="sxs-lookup"><span data-stu-id="42e6e-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="42e6e-252">Также попробуйте использовать другой браузер, например Internet Explorer или Edge, где hello проблема не возникает.</span><span class="sxs-lookup"><span data-stu-id="42e6e-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
