---
title: "Веб-приложение с Express (Node.js) | Документация Майкрософт"
description: "Этот учебник основывается на учебнике по облачным службам и демонстрирует использование модуля Express."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="8a779-103">Создание веб-приложения Node.js с использованием модуля Express в облачной службе Azure</span><span class="sxs-lookup"><span data-stu-id="8a779-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="8a779-104">Node.js включает минимальный набор функциональных возможностей в базовой среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="8a779-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="8a779-105">Разработчики часто используют сторонние модули для получения дополнительной функциональности при разработке приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="8a779-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="8a779-106">В этом руководстве будет создано новое приложение с помощью модуля [Express][Express], который предоставляет платформу MVC для создания веб-приложений Node.js.</span><span class="sxs-lookup"><span data-stu-id="8a779-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="8a779-107">Снимок экрана завершенного приложения приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="8a779-107">A screenshot of the completed application is below:</span></span>

![Веб-браузер, отображающий приветствие модуля Express в Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="8a779-109">Создание проекта облачной службы</span><span class="sxs-lookup"><span data-stu-id="8a779-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="8a779-110">Чтобы создать новый проект облачной службы с именем expressapp, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8a779-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="8a779-111">В **меню Пуск** или на **начальном экране** найдите **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8a779-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="8a779-112">Щелкните правой кнопкой мыши **Windows PowerShell** и выберите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="8a779-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Значок Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="8a779-114">Перейдите в каталог **c:\\node**, а затем введите указанные ниже команды для создания решения с именем **expressapp** и рабочей роли с именем **WebRole1**.</span><span class="sxs-lookup"><span data-stu-id="8a779-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="8a779-115">По умолчанию **Add-AzureNodeWebRole** использует предыдущую версию Node.js.</span><span class="sxs-lookup"><span data-stu-id="8a779-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="8a779-116">Показанная выше инструкция **Set-AzureServiceProjectRole** предписывает Azure использовать Node v0.10.21.</span><span class="sxs-lookup"><span data-stu-id="8a779-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="8a779-117">Обратите внимание, что параметры зависят от регистра.</span><span class="sxs-lookup"><span data-stu-id="8a779-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="8a779-118">Можно проверить, выбрана ли правильная версия Node.js, выбрав свойство **engines** в **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="8a779-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="8a779-119">Установка модуля Express</span><span class="sxs-lookup"><span data-stu-id="8a779-119">Install Express</span></span>
1. <span data-ttu-id="8a779-120">Установите генератор Express, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a779-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="8a779-121">Результат команды npm должен соответствовать показанному ниже результату.</span><span class="sxs-lookup"><span data-stu-id="8a779-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Windows PowerShell с выходными данными команды npm install express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="8a779-123">Перейдите в каталог **WebRole1** и используйте команду express для создания нового приложения.</span><span class="sxs-lookup"><span data-stu-id="8a779-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="8a779-124">Вам будет предложено перезаписать более раннюю версию приложения.</span><span class="sxs-lookup"><span data-stu-id="8a779-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="8a779-125">Для продолжения введите **y** или **yes**.</span><span class="sxs-lookup"><span data-stu-id="8a779-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="8a779-126">Модуль Express сформирует файл app.js и структуру папок для создания вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="8a779-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![Результат команды express](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="8a779-128">Чтобы установить дополнительные зависимости, определенные в файле package.json, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a779-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Результат команды npm install](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="8a779-130">Скопируйте файл **bin/www** в **server.js** с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="8a779-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="8a779-131">Таким образом, облачная служба сможет найти точку входа в это приложение.</span><span class="sxs-lookup"><span data-stu-id="8a779-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="8a779-132">После выполнения команды файл **server.js** должен содержаться в каталоге WebRole1.</span><span class="sxs-lookup"><span data-stu-id="8a779-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="8a779-133">В файле **server.js** удалите одну из точек (символ ".") из строки, приведенной ниже.</span><span class="sxs-lookup"><span data-stu-id="8a779-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="8a779-134">После сделанных изменений строка должна выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="8a779-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="8a779-135">Это необходимо сделать, так как мы перенесли файл (ранее **bin/www**) в тот же каталог, в котором должен находиться файл приложения.</span><span class="sxs-lookup"><span data-stu-id="8a779-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="8a779-136">После внесения изменений сохраните файл **server.js** .</span><span class="sxs-lookup"><span data-stu-id="8a779-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="8a779-137">Выполнив следующую команду, запустите приложение в эмуляторе Azure:</span><span class="sxs-lookup"><span data-stu-id="8a779-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Веб-страница, содержащая приветствие модуля express.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="8a779-139">Изменение представления</span><span class="sxs-lookup"><span data-stu-id="8a779-139">Modifying the View</span></span>
<span data-ttu-id="8a779-140">Теперь измените представление для отображения сообщения «Вас приветствует Express в Azure».</span><span class="sxs-lookup"><span data-stu-id="8a779-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="8a779-141">Чтобы открыть файл index.jade, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a779-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Содержимое файла index.jade.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="8a779-143">Jade — это обработчик представлений по умолчанию, используемый приложениями Express.</span><span class="sxs-lookup"><span data-stu-id="8a779-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="8a779-144">Дополнительные сведения об обработчике представлений Jade см. на сайте [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="8a779-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="8a779-145">Измените последнюю строку текста, добавив слова **in Azure**.</span><span class="sxs-lookup"><span data-stu-id="8a779-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![Файл index.jade, последняя строка содержит текст: p Welcome to \#{title} in Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="8a779-147">Сохраните файл и выйдите из Блокнота.</span><span class="sxs-lookup"><span data-stu-id="8a779-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="8a779-148">Обновите браузер и увидите изменения.</span><span class="sxs-lookup"><span data-stu-id="8a779-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Окно браузера со страницей приветствия Express в Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="8a779-150">После тестирования приложения остановите эмулятор с помощью командлета **Stop-AzureEmulator** .</span><span class="sxs-lookup"><span data-stu-id="8a779-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="8a779-151">Публикация приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="8a779-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="8a779-152">В окне Azure PowerShell используйте командлет **Publish-AzureServiceProject** , чтобы развернуть приложение в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="8a779-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="8a779-153">После завершения операции развертывания откроется браузер с отображением веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="8a779-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![В веб-браузере отображается страница Express.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="8a779-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a779-156">Next steps</span></span>
<span data-ttu-id="8a779-157">Дополнительную информацию см. в [центре разработчиков Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="8a779-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


