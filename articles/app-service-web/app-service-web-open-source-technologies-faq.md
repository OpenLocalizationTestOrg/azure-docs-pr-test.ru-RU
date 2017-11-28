---
title: "Часто задаваемые вопросы о технологиях с открытым кодом в веб-приложениях Azure | Документация Майкрософт"
description: "Ответы на часто задаваемые вопросы о технологиях с открытым кодом в веб-приложениях службы приложений Azure."
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
ms.openlocfilehash: d37b53242c0b231d83425a59ecbe50216216a95b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="5cd75-103">Часто задаваемые вопросы о технологиях с открытым кодом в веб-приложениях Azure</span><span class="sxs-lookup"><span data-stu-id="5cd75-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="5cd75-104">В этой статье содержатся ответы на часто задаваемые вопросы о проблемах, связанных с технологиями с открытым кодом, в [веб-приложениях службы приложений Azure](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-104">This article has answers to frequently asked questions (FAQs) about issues with open-source technologies for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="5cd75-105">База данных ClearDB не работает.</span><span class="sxs-lookup"><span data-stu-id="5cd75-105">My ClearDB database is down.</span></span> <span data-ttu-id="5cd75-106">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="5cd75-106">How do I resolve this?</span></span>

<span data-ttu-id="5cd75-107">По вопросам, связанным с базами данных, обращайтесь в [службу поддержки ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="5cd75-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="5cd75-108">Ответы на часто задаваемые вопросы о базе данных ClearDB см. в [этой статье](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-108">For answers to common questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-the-portal"></a><span data-ttu-id="5cd75-109">Почему база данных ClearDB не отображается на портале?</span><span class="sxs-lookup"><span data-stu-id="5cd75-109">Why isn't my ClearDB database listed in the portal?</span></span>

<span data-ttu-id="5cd75-110">Если вы создали базу данных ClearDB на [портале Azure](http://portal.azure.com/), она не отображается на [классическом портале Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-110">If you create a ClearDB database in the [Azure portal](http://portal.azure.com/), the database doesn't appear in the [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="5cd75-111">Чтобы решить эту проблему, вручную свяжите нужную базу данных с веб-приложением.</span><span class="sxs-lookup"><span data-stu-id="5cd75-111">To work around this, you can manually link your database to the web app.</span></span>

<span data-ttu-id="5cd75-112">Аналогично, если вы создали базу данных ClearDB на [классическом портале Azure](http://manage.windowsazure.com/), она не отображается на [портале Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-112">Similarly, if you create a ClearDB database in the [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in the [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="5cd75-113">Для этой ситуации нет решения.</span><span class="sxs-lookup"><span data-stu-id="5cd75-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="5cd75-114">Дополнительные сведения см. в статье [Часто задаваемые вопросы о базах данных ClearDB MySql в службе приложений Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="5cd75-115">Почему не удалось перенести базу данных ClearDB при переносе подписки?</span><span class="sxs-lookup"><span data-stu-id="5cd75-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="5cd75-116">При переносе ресурсов из одной подписки в другую действуют некоторые ограничения.</span><span class="sxs-lookup"><span data-stu-id="5cd75-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="5cd75-117">База данных ClearDB MySQL — это сторонняя служба, и она не перемещается при переносе подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd75-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="5cd75-118">Если вы не перенесли базу данных MySQL до переноса ресурсов Azure, база данных ClearDB MySQL может быть недоступной.</span><span class="sxs-lookup"><span data-stu-id="5cd75-118">If you don't manage the migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="5cd75-119">Чтобы избежать этого, сначала вручную перенесите свою базу данных ClearDB, а затем перенесите подписку веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd75-119">To avoid this, first, manually migrate your ClearDB database, and then migrate the Azure subscription for your web app.</span></span>

<span data-ttu-id="5cd75-120">Дополнительные сведения см. в статье [Часто задаваемые вопросы о базах данных ClearDB MySql в службе приложений Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-to-troubleshoot-php-issues"></a><span data-ttu-id="5cd75-121">Как включить ведение журнала PHP, чтобы устранить неполадки с приложением PHP?</span><span class="sxs-lookup"><span data-stu-id="5cd75-121">How do I turn on PHP logging to troubleshoot PHP issues?</span></span>

<span data-ttu-id="5cd75-122">Чтобы включить ведение журнала PHP, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5cd75-122">To turn on PHP logging:</span></span>

1. <span data-ttu-id="5cd75-123">Перейдите на [веб-сайт Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="5cd75-123">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="5cd75-124">В верхнем меню выберите **Консоль отладки** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-124">In the top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="5cd75-125">Выберите папку **Site**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-125">Select the **Site** folder.</span></span>
4. <span data-ttu-id="5cd75-126">Выберите папку **wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-126">Select the **wwwroot** folder.</span></span>
5. <span data-ttu-id="5cd75-127">Щелкните значок **+**, а затем выберите **Создать файл**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-127">Select the **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="5cd75-128">Задайте файлу имя **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-128">Set the file name to **.user.ini**.</span></span>
7. <span data-ttu-id="5cd75-129">Щелкните значок карандаша рядом с файлом **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-129">Select the pencil icon next to **.user.ini**.</span></span>
8. <span data-ttu-id="5cd75-130">Добавьте в файл следующий код: `log_errors=on`.</span><span class="sxs-lookup"><span data-stu-id="5cd75-130">In the file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="5cd75-131">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-131">Select **Save**.</span></span>
10. <span data-ttu-id="5cd75-132">Щелкните значок карандаша рядом с файлом **wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-132">Select the pencil icon next to **wp-config.php**.</span></span>
11. <span data-ttu-id="5cd75-133">Вместо текста в файле добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="5cd75-133">Change the text to the following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging to /wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings to screendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors to screenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="5cd75-134">На портале Azure в меню веб-приложения перезапустите свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="5cd75-134">In the Azure portal, in the web app menu, restart your web app.</span></span>

<span data-ttu-id="5cd75-135">Дополнительные сведения см. в записи блога [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Включение журналов ошибок WordPress).</span><span class="sxs-lookup"><span data-stu-id="5cd75-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="5cd75-136">Как включить ведение журнала ошибок в приложениях Python, размещенных в службе приложений?</span><span class="sxs-lookup"><span data-stu-id="5cd75-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="5cd75-137">Чтобы включить запись ошибок в приложении Python, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5cd75-137">To capture Python application errors:</span></span>

1. <span data-ttu-id="5cd75-138">На портале Azure перейдите к своему веб-приложению и выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-138">In the Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="5cd75-139">На вкладке **Параметры** щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-139">On the **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="5cd75-140">В разделе **Параметры приложения** введите следующую пару "ключ — значение":</span><span class="sxs-lookup"><span data-stu-id="5cd75-140">Under **App settings**, enter the following key/value pair:</span></span>
    * <span data-ttu-id="5cd75-141">Ключ: WSGI_LOG.</span><span class="sxs-lookup"><span data-stu-id="5cd75-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="5cd75-142">Значение: D:\home\site\wwwroot\logs.txt (введите собственное имя файла).</span><span class="sxs-lookup"><span data-stu-id="5cd75-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="5cd75-143">Теперь ошибки должны отображаться в файле logs.txt в папке wwwroot.</span><span class="sxs-lookup"><span data-stu-id="5cd75-143">You should now see errors in the logs.txt file in the wwwroot folder.</span></span>

## <a name="how-do-i-change-the-version-of-the-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="5cd75-144">Как изменить версию приложения Node.js, размещенного в службе приложений?</span><span class="sxs-lookup"><span data-stu-id="5cd75-144">How do I change the version of the Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="5cd75-145">Версию приложения Node.js можно изменить одним из следующих методов:</span><span class="sxs-lookup"><span data-stu-id="5cd75-145">To change the version of the Node.js application, you can use one of the following options:</span></span>

*   <span data-ttu-id="5cd75-146">На портале Azure в меню **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-146">In the Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="5cd75-147">Откройте портал Azure и перейдите к своему веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="5cd75-147">In the Azure portal, go to your web app.</span></span>
    2. <span data-ttu-id="5cd75-148">В колонке **Параметры** щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="5cd75-148">On the **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="5cd75-149">В разделе **Параметры приложения** добавьте WEBSITE_NODE_DEFAULT_VERSION в качестве ключа и укажите необходимую версию Node.js в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="5cd75-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as the key, and the version of Node.js you want as the value.</span></span>
    4. <span data-ttu-id="5cd75-150">Откройте [консоль Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="5cd75-150">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="5cd75-151">Чтобы проверить версию Node.js, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="5cd75-151">To check the Node.js version, enter the following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="5cd75-152">Измените файл iisnode.yml.</span><span class="sxs-lookup"><span data-stu-id="5cd75-152">Modify the iisnode.yml file.</span></span> <span data-ttu-id="5cd75-153">Если изменить версию Node.js в файле iisnode.yml, вы зададите только среду выполнения, используемую IISNode.</span><span class="sxs-lookup"><span data-stu-id="5cd75-153">Changing the Node.js version in the iisnode.yml file only sets the runtime environment that iisnode uses.</span></span> <span data-ttu-id="5cd75-154">Командная строка Kudu и остальные компоненты по-прежнему будут использовать версию Node.js, заданную в разделе **Параметры приложения** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd75-154">Your Kudu cmd and others still use the Node.js version that is set in **App settings** in the Azure portal.</span></span>

    <span data-ttu-id="5cd75-155">Чтобы вручную задать файл iisnode.yml, создайте файл iisnode.yml в корневой папке приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd75-155">To set the iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="5cd75-156">Добавьте в этот файл следующую строку:</span><span class="sxs-lookup"><span data-stu-id="5cd75-156">In the file, include the following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="5cd75-157">Задайте файл iisnode.yml с помощью файла package.json во время развертывания системы управления версиями.</span><span class="sxs-lookup"><span data-stu-id="5cd75-157">Set the iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="5cd75-158">Процесс развертывания системы управления версиями Azure состоит из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="5cd75-158">The Azure source control deployment process involves the following steps:</span></span>
    1. <span data-ttu-id="5cd75-159">Перемещение содержимого в веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd75-159">Moves content to the Azure web app.</span></span>
    2. <span data-ttu-id="5cd75-160">Создание скрипта развертывания по умолчанию, если его нет (файл deploy.cmd) в корневой папке веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd75-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in the web app root folder.</span></span>
    3. <span data-ttu-id="5cd75-161">Выполнение скрипта развертывания, который создает файл iisnode.yml, если вы указали версию Node.js в файле package.json в строке `"engines": {"node": "5.9.1","npm": "3.7.3"}`.</span><span class="sxs-lookup"><span data-stu-id="5cd75-161">Runs a deployment script in which it creates an iisnode.yml file if you mention the Node.js version in the package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="5cd75-162">Файл iisnode.yml содержит следующую строку кода:</span><span class="sxs-lookup"><span data-stu-id="5cd75-162">The iisnode.yml file has the following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-the-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="5cd75-163">В приложении WordPress, размещенном в службе приложений, отображается сообщение Error establishing a database connection (Ошибка при установке подключения к базе данных).</span><span class="sxs-lookup"><span data-stu-id="5cd75-163">I see the message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="5cd75-164">Как устранить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="5cd75-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="5cd75-165">При появлении этой ошибки в приложении Azure WordPress необходимо включить файлы php_errors.log и debug.log. Для этого выполните действия, описанные в записи блога [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (Включение журналов ошибок WordPress).</span><span class="sxs-lookup"><span data-stu-id="5cd75-165">If you see this error in your Azure WordPress app, to enable php_errors.log and debug.log, complete the steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="5cd75-166">После включения журналов воспроизведите ошибку и проверьте журналы:</span><span class="sxs-lookup"><span data-stu-id="5cd75-166">When the logs are enabled, reproduce the error, and then check the logs to see if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded the ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="5cd75-167">Если в файле debug.log или php_errors.log отображается приведенное выше сообщение об ошибке, это означает, что приложение превысило количество доступных подключений.</span><span class="sxs-lookup"><span data-stu-id="5cd75-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding the number of connections.</span></span> <span data-ttu-id="5cd75-168">При использовании базы данных ClearDB проверьте доступное количество подключений для вашего [плана обслуживания](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="5cd75-168">If you’re hosting on ClearDB, verify the number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="5cd75-169">Как отлаживать приложение Node.js, размещенное в службе приложений?</span><span class="sxs-lookup"><span data-stu-id="5cd75-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="5cd75-170">Откройте [консоль Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="5cd75-170">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="5cd75-171">Перейдите к папке журналов приложений (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="5cd75-171">Go to your application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="5cd75-172">Проверьте содержимое файла logging_errors.txt.</span><span class="sxs-lookup"><span data-stu-id="5cd75-172">In the logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="5cd75-173">Как установить собственные модули Python в веб-приложении службы приложений или приложении API?</span><span class="sxs-lookup"><span data-stu-id="5cd75-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="5cd75-174">Некоторые пакеты невозможно установить с помощью pip в Azure.</span><span class="sxs-lookup"><span data-stu-id="5cd75-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="5cd75-175">Эти пакеты могут быть недоступны в индексе пакетов Python, или требуется компилятор (компилятор недоступен на компьютере, на котором выполняется веб-приложение в службе приложений).</span><span class="sxs-lookup"><span data-stu-id="5cd75-175">The package might not be available on the Python Package Index, or a compiler might be required (a compiler is not available on the computer that is running the web app in App Service).</span></span> <span data-ttu-id="5cd75-176">Сведения об установке собственных модулей в веб-приложениях службы приложений или приложениях API см. в [этой записи блога](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-to-app-service-by-using-git-and-the-new-version-of-python"></a><span data-ttu-id="5cd75-177">Как развернуть приложение Django в службу приложений с помощью Git и новой версии Python?</span><span class="sxs-lookup"><span data-stu-id="5cd75-177">How do I deploy a Django app to App Service by using Git and the new version of Python?</span></span>

<span data-ttu-id="5cd75-178">Сведения об установке Django см. в [этой записи блога](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-178">For information about installing Django, see [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-the-tomcat-log-files-located"></a><span data-ttu-id="5cd75-179">Где находятся файлы журналов Tomcat?</span><span class="sxs-lookup"><span data-stu-id="5cd75-179">Where are the Tomcat log files located?</span></span>

<span data-ttu-id="5cd75-180">Для развертываний Microsoft Azure Marketplace и пользовательских развертываний:</span><span class="sxs-lookup"><span data-stu-id="5cd75-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="5cd75-181">Расположение папки: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs.</span><span class="sxs-lookup"><span data-stu-id="5cd75-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="5cd75-182">Необходимые файлы:</span><span class="sxs-lookup"><span data-stu-id="5cd75-182">Files of interest:</span></span>
    * <span data-ttu-id="5cd75-183">catalina.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="5cd75-184">host-manager.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="5cd75-185">localhost.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="5cd75-186">manager.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="5cd75-187">site_access_log.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="5cd75-188">Для развертываний из меню **Параметры приложения** портала:</span><span class="sxs-lookup"><span data-stu-id="5cd75-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="5cd75-189">Расположение папки: D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="5cd75-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="5cd75-190">Необходимые файлы:</span><span class="sxs-lookup"><span data-stu-id="5cd75-190">Files of interest:</span></span>
    * <span data-ttu-id="5cd75-191">catalina.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="5cd75-192">host-manager.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="5cd75-193">localhost.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="5cd75-194">manager.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="5cd75-195">site_access_log.*ГГГГ-ММ-ДД*.log</span><span class="sxs-lookup"><span data-stu-id="5cd75-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="5cd75-196">Как устранить ошибки подключения драйвера JDBC Driver?</span><span class="sxs-lookup"><span data-stu-id="5cd75-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="5cd75-197">В журналах Tomcat может появиться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="5cd75-197">You might see the following message in your Tomcat logs:</span></span>

```
The web application[ROOT] registered the JDBC driver [com.mysql.jdbc.Driver] but failed to unregister it when the web application was stopped. To prevent a memory leak,the JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="5cd75-198">Чтобы устранить эту ошибку, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5cd75-198">To resolve the error:</span></span>

1. <span data-ttu-id="5cd75-199">Удалите файл sqljdbc*.jar из папки app/lib.</span><span class="sxs-lookup"><span data-stu-id="5cd75-199">Remove the sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="5cd75-200">При использовании пользовательского веб-сервера Tomcat или веб-сервера Tomcat из Microsoft Azure Marketplace скопируйте этот JAR-файл в папку lib.</span><span class="sxs-lookup"><span data-stu-id="5cd75-200">If you are using the custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file to the Tomcat lib folder.</span></span>
3. <span data-ttu-id="5cd75-201">При включении Java на портале Azure (выберите **Java 1.8** > **Tomcat server** (Сервер Tomcat)) скопируйте файл sqljdbc.* jar в папку, связанную с приложением.</span><span class="sxs-lookup"><span data-stu-id="5cd75-201">If you are enabling Java from the Azure portal (select **Java 1.8** > **Tomcat server**), copy the sqljdbc.* jar file in the folder that's parallel to your app.</span></span> <span data-ttu-id="5cd75-202">Затем добавьте в файл web.config следующий параметр classpath:</span><span class="sxs-lookup"><span data-stu-id="5cd75-202">Then, add the following classpath setting to the web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path to the sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-to-copy-live-log-files"></a><span data-ttu-id="5cd75-203">Почему возникают ошибки при попытке скопировать динамические файлы журналов?</span><span class="sxs-lookup"><span data-stu-id="5cd75-203">Why do I see errors when I attempt to copy live log files?</span></span>

<span data-ttu-id="5cd75-204">При попытке скопировать динамические файлы журналов приложения Java (например, Tomcat) может отображаться следующая ошибка FTP:</span><span class="sxs-lookup"><span data-stu-id="5cd75-204">If you try to copy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
The process cannot access the file because it is being used by another process.
```

<span data-ttu-id="5cd75-205">Сообщение об ошибке может отличаться в зависимости от FTP-клиента.</span><span class="sxs-lookup"><span data-stu-id="5cd75-205">The error message might vary, depending on the FTP client.</span></span>

<span data-ttu-id="5cd75-206">Все приложения Java имеют эту проблему.</span><span class="sxs-lookup"><span data-stu-id="5cd75-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="5cd75-207">Только приложения Kudu поддерживают загрузку этого файла во время выполнения приложения.</span><span class="sxs-lookup"><span data-stu-id="5cd75-207">Only Kudu supports downloading this file while the app is running.</span></span>

<span data-ttu-id="5cd75-208">Чтобы предоставить к этим файлам доступ по протоколу FTP, остановите приложение.</span><span class="sxs-lookup"><span data-stu-id="5cd75-208">Stopping the app allows FTP access to these files.</span></span>

<span data-ttu-id="5cd75-209">Кроме того, вы можете написать веб-задание, которое будет копировать эти файлы в другой каталог по установленному расписанию.</span><span class="sxs-lookup"><span data-stu-id="5cd75-209">Another workaround is to write a WebJob that runs on a schedule and copies these files to a different directory.</span></span> <span data-ttu-id="5cd75-210">Пример проекта см. [здесь](https://github.com/kamilsykora/CopyLogsJob).</span><span class="sxs-lookup"><span data-stu-id="5cd75-210">For a sample project, see the [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-the-log-files-for-jetty"></a><span data-ttu-id="5cd75-211">Где найти файлы журналов для Jetty?</span><span class="sxs-lookup"><span data-stu-id="5cd75-211">Where do I find the log files for Jetty?</span></span>

<span data-ttu-id="5cd75-212">Файл журнала для развертываний Microsoft Azure Marketplace и пользовательских развертываний расположен в папке D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs.</span><span class="sxs-lookup"><span data-stu-id="5cd75-212">For Marketplace and custom deployments, the log file is in the D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="5cd75-213">Обратите внимание, что расположение папки зависит от используемой версии Jetty.</span><span class="sxs-lookup"><span data-stu-id="5cd75-213">Note that the folder location depends on the version of Jetty you are using.</span></span> <span data-ttu-id="5cd75-214">Например, приведенный выше путь предназначен для Jetty версии 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="5cd75-214">For example, the path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="5cd75-215">Найдите файл jetty_*ГГГГ_ММ_ДД*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="5cd75-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="5cd75-216">Файл журнала для развертываний из меню "Параметры приложения" портала находится в папке D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="5cd75-216">For portal App Setting deployments, the log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="5cd75-217">Найдите файл jetty_*ГГГГ_ММ_ДД*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="5cd75-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="5cd75-218">Можно ли отправлять электронные сообщения из веб-приложения Azure?</span><span class="sxs-lookup"><span data-stu-id="5cd75-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="5cd75-219">Служба приложений не имеет встроенной функции отправки электронных сообщений.</span><span class="sxs-lookup"><span data-stu-id="5cd75-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="5cd75-220">Альтернативные варианты отправки электронных сообщений из приложения см. в [этом обсуждении Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="5cd75-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-to-another-url"></a><span data-ttu-id="5cd75-221">Почему сайт WordPress перенаправляет на другой URL-адрес?</span><span class="sxs-lookup"><span data-stu-id="5cd75-221">Why does my WordPress site redirect to another URL?</span></span>

<span data-ttu-id="5cd75-222">Если вы недавно перенесли свои ресурсы в Azure, WordPress может перенаправлять на старый URL-адрес домена.</span><span class="sxs-lookup"><span data-stu-id="5cd75-222">If you have recently migrated to Azure, WordPress might redirect to the old domain URL.</span></span> <span data-ttu-id="5cd75-223">Это вызвано конфигурацией базы данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="5cd75-223">This is caused by a setting in the MySQL database.</span></span>

<span data-ttu-id="5cd75-224">WordPress Buddy+ — это расширение сайта Azure, с помощью которого можно обновить URL-адрес перенаправления непосредственно в базе данных.</span><span class="sxs-lookup"><span data-stu-id="5cd75-224">WordPress Buddy+ is an Azure Site Extension that you can use to update the redirection URL directly in the database.</span></span> <span data-ttu-id="5cd75-225">Дополнительные сведения об использовании WordPress Buddy+ см. в записи блога [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Средства WordPress и перенос базы данных MySQL с помощью WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="5cd75-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="5cd75-226">Кроме того, если вы предпочитаете вручную обновить URL-адрес перенаправления с помощью SQL-запросов или PHPMyAdmin, см. запись блога [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/) (WordPress: перенаправление на неправильный URL-адрес).</span><span class="sxs-lookup"><span data-stu-id="5cd75-226">Alternatively, if you prefer to manually update the redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="5cd75-227">Как изменить пароль для входа в WordPress?</span><span class="sxs-lookup"><span data-stu-id="5cd75-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="5cd75-228">Если вы забыли пароль для входа в WordPress, его можно обновить с помощью WordPress Buddy+.</span><span class="sxs-lookup"><span data-stu-id="5cd75-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ to update it.</span></span> <span data-ttu-id="5cd75-229">Чтобы сбросить пароль, установите расширение сайта Azure WordPress Buddy+, а затем выполните действия, описанные в записи блога [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Средства WordPress и перенос базы данных MySQL с помощью WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="5cd75-229">To reset your password, install the WordPress Buddy+ Azure Site Extension, and then complete the steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-to-wordpress-how-do-i-resolve-this"></a><span data-ttu-id="5cd75-230">Не удается войти в WordPress.</span><span class="sxs-lookup"><span data-stu-id="5cd75-230">I can't sign in to WordPress.</span></span> <span data-ttu-id="5cd75-231">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="5cd75-231">How do I resolve this?</span></span>

<span data-ttu-id="5cd75-232">Если вы не можете войти в WordPress после установки подключаемого модуля, возможно, вы установили не тот модуль.</span><span class="sxs-lookup"><span data-stu-id="5cd75-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="5cd75-233">WordPress Buddy+ — это расширение сайта Azure, с помощью которого можно отключить подключаемые модули в WordPress.</span><span class="sxs-lookup"><span data-stu-id="5cd75-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="5cd75-234">Дополнительные сведения см. в записи блога [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (Средства WordPress и перенос базы данных MySQL с помощью WordPress Buddy+).</span><span class="sxs-lookup"><span data-stu-id="5cd75-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="5cd75-235">Как перенести базу данных WordPress?</span><span class="sxs-lookup"><span data-stu-id="5cd75-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="5cd75-236">Базу данных MySQL, подключенную к веб-сайту WordPress, можно перенести несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="5cd75-236">You have multiple options for migrating the MySQL database that's connected to your WordPress website:</span></span>

* <span data-ttu-id="5cd75-237">с помощью [командной строки или PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/) (для разработчиков);</span><span class="sxs-lookup"><span data-stu-id="5cd75-237">Developers: Use the [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="5cd75-238">с помощью [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (остальные пользователи).</span><span class="sxs-lookup"><span data-stu-id="5cd75-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="5cd75-239">Как повысить уровень защиты WordPress?</span><span class="sxs-lookup"><span data-stu-id="5cd75-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="5cd75-240">Рекомендации по обеспечению безопасности WordPress см. в [этой записи блога](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="5cd75-240">To learn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-to-use-phpmyadmin-and-i-see-the-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="5cd75-241">При использовании PHPMyAdmin отображается ошибка "Доступ запрещен".</span><span class="sxs-lookup"><span data-stu-id="5cd75-241">I am trying to use PHPMyAdmin, and I see the message “Access denied.”</span></span> <span data-ttu-id="5cd75-242">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="5cd75-242">How do I resolve this?</span></span>

<span data-ttu-id="5cd75-243">Эта проблема может возникать, если компонент MySQL приложения еще не запущен в этом экземпляре службы приложений.</span><span class="sxs-lookup"><span data-stu-id="5cd75-243">You might experience this issue if the MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="5cd75-244">Чтобы устранить эту проблему, попробуйте получить доступ к веб-сайту.</span><span class="sxs-lookup"><span data-stu-id="5cd75-244">To resolve the issue, try to access your website.</span></span> <span data-ttu-id="5cd75-245">При этом запустятся необходимые процессы, в том числе процессы MySQL в приложении.</span><span class="sxs-lookup"><span data-stu-id="5cd75-245">This starts the required processes, including the MySQL in-app process.</span></span> <span data-ttu-id="5cd75-246">Чтобы проверить, выполняется ли MySQL в приложении, найдите процесс mysqld.exe в списке процессов в обозревателе процессов.</span><span class="sxs-lookup"><span data-stu-id="5cd75-246">To verify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in the processes.</span></span>

<span data-ttu-id="5cd75-247">Если MySQL выполняется, попробуйте запустить PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="5cd75-247">After you ensure that MySQL in-app is running, try to use PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-to-import-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="5cd75-248">При попытке импорта или экспорта базы данных MySQL в приложении с помощью PHPMyadmin произошла ошибка HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="5cd75-248">I get an HTTP 403 error when I try to import or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="5cd75-249">Как решить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="5cd75-249">How do I resolve this?</span></span>

<span data-ttu-id="5cd75-250">Это известная ошибка в старой версии браузера Chrome.</span><span class="sxs-lookup"><span data-stu-id="5cd75-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="5cd75-251">Чтобы устранить эту проблему, обновите браузер Chrome.</span><span class="sxs-lookup"><span data-stu-id="5cd75-251">To resolve the issue, upgrade to a newer version of Chrome.</span></span> <span data-ttu-id="5cd75-252">Кроме того, попробуйте использовать другой браузер, например Internet Explorer или Edge, где эта проблема не возникает.</span><span class="sxs-lookup"><span data-stu-id="5cd75-252">Also try using a different browser, like Internet Explorer or Edge, where the issue does not occur.</span></span>
