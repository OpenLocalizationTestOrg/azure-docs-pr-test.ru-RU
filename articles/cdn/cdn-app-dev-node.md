---
title: "Приступая к работе с пакетом SDK Azure CDN для Node.js | Документация Майкрософт"
description: "Узнайте, как создать приложение Node.js для управления Azure CDN."
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 46ae8cd9775432d126cbde856c1fb06ea319297e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="acb5e-103">Приступая к разработке для Azure CDN</span><span class="sxs-lookup"><span data-stu-id="acb5e-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="acb5e-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="acb5e-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="acb5e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="acb5e-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="acb5e-106">С помощью [пакета SDK Azure CDN для Node.js](https://www.npmjs.com/package/azure-arm-cdn) можно автоматизировать создание профилей и конечных точек CDN и управление ими.</span><span class="sxs-lookup"><span data-stu-id="acb5e-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="acb5e-107">В этом руководстве описывается создание простого консольного приложения Node.js с примерами некоторых доступных операций.</span><span class="sxs-lookup"><span data-stu-id="acb5e-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="acb5e-108">Это руководство не содержит подробные сведения обо всех свойствах пакета Azure CDN SDK для Node.js.</span><span class="sxs-lookup"><span data-stu-id="acb5e-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="acb5e-109">Для работы с этим учебником должен быть установлен и настроен компонент [Node.js](http://www.nodejs.org) **4.x.x** или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="acb5e-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="acb5e-110">Для создания приложения Node.js вы можете использовать любой текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="acb5e-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="acb5e-111">Например, в этом учебнике используется [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="acb5e-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="acb5e-112">[Завершенный проект из этого учебника](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) доступен для скачивания на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="acb5e-112">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="acb5e-113">Создание проекта и добавление зависимостей NPM</span><span class="sxs-lookup"><span data-stu-id="acb5e-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="acb5e-114">Создав группу ресурсов для профилей CDN и назначив приложению Azure AD разрешения для управления профилями CDN и конечными точками в этой группе, мы можем приступить к созданию своего приложения.</span><span class="sxs-lookup"><span data-stu-id="acb5e-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="acb5e-115">Создайте папку для хранения приложения.</span><span class="sxs-lookup"><span data-stu-id="acb5e-115">Create a folder to store your application.</span></span>  <span data-ttu-id="acb5e-116">С помощью консоли, в которой средства Node.js включены в текущий путь, перейдите в эту новую папку и инициализируйте проект с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="acb5e-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="acb5e-117">Вам будет предложено ответить на ряд вопросов для инициализации проекта.</span><span class="sxs-lookup"><span data-stu-id="acb5e-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="acb5e-118">В качестве **точки входа**в этом руководстве используется *app.js*.</span><span class="sxs-lookup"><span data-stu-id="acb5e-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="acb5e-119">В приведенном ниже примере вы можете увидеть значения других параметров.</span><span class="sxs-lookup"><span data-stu-id="acb5e-119">You can see my other choices in the following example.</span></span>

![Выходные данные NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="acb5e-121">Теперь наш проект будет инициализирован с помощью файла *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="acb5e-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="acb5e-122">В проекте будут использоваться некоторые библиотеки Azure, содержащиеся в пакетах NPM.</span><span class="sxs-lookup"><span data-stu-id="acb5e-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="acb5e-123">Мы будем использовать клиентскую среду Azure для Node.js (ms-rest-azure) и клиентскую библиотеку Azure CDN для Node.js (azure-arm-cd).</span><span class="sxs-lookup"><span data-stu-id="acb5e-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="acb5e-124">Давайте добавим эти зависимости в проект.</span><span class="sxs-lookup"><span data-stu-id="acb5e-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="acb5e-125">Когда установка этих пакетов завершится, файл *package.json* должен выглядеть примерно так (номер версии может отличаться):</span><span class="sxs-lookup"><span data-stu-id="acb5e-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

<span data-ttu-id="acb5e-126">И, наконец, создайте с помощью текстового редактора пустой текстовый файл и сохраните его с именем *app.js*в корневой папке проекта.</span><span class="sxs-lookup"><span data-stu-id="acb5e-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="acb5e-127">Теперь мы готовы приступить к написанию кода.</span><span class="sxs-lookup"><span data-stu-id="acb5e-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="acb5e-128">Требования, константы, проверка подлинности и структура</span><span class="sxs-lookup"><span data-stu-id="acb5e-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="acb5e-129">Давайте откроем файл *app.js* в редакторе и создадим базовую структуру нашей программы.</span><span class="sxs-lookup"><span data-stu-id="acb5e-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="acb5e-130">В начале файла добавьте строки required для всех наших пакетов NPM:</span><span class="sxs-lookup"><span data-stu-id="acb5e-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="acb5e-131">Необходимо определить несколько констант, которые будут использоваться нашими методами.</span><span class="sxs-lookup"><span data-stu-id="acb5e-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="acb5e-132">Добавьте следующий код.</span><span class="sxs-lookup"><span data-stu-id="acb5e-132">Add the following.</span></span>  <span data-ttu-id="acb5e-133">Обязательно замените заполнители, включая **&lt;угловые скобки&gt;**, собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="acb5e-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="acb5e-134">Далее мы создадим клиент управления CDN и передадим ему наши учетные данные.</span><span class="sxs-lookup"><span data-stu-id="acb5e-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="acb5e-135">Если вы используете аутентификацию отдельных пользователей, эти две строки будут выглядеть немного иначе.</span><span class="sxs-lookup"><span data-stu-id="acb5e-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="acb5e-136">Используйте приведенный пример кода, только если решили использовать аутентификацию отдельных пользователей, а не субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="acb5e-136">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="acb5e-137">Следите за тем, чтобы ваши учетные данные пользователя хранились в секрете.</span><span class="sxs-lookup"><span data-stu-id="acb5e-137">Be careful to guard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="acb5e-138">Не забудьте заменить правильными данными все элементы в **&lt;угловых скобках&gt;**.</span><span class="sxs-lookup"><span data-stu-id="acb5e-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="acb5e-139">Вместо `<redirect URI>`укажите универсальный код ресурса (URI) перенаправления, который вы ввели при регистрации приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="acb5e-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="acb5e-140">Консольное приложение Node.js будет принимать некоторые параметры командной строки.</span><span class="sxs-lookup"><span data-stu-id="acb5e-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="acb5e-141">Давайте добавим проверку того, что передан хотя бы один параметр.</span><span class="sxs-lookup"><span data-stu-id="acb5e-141">Let's validate that at least one parameter was passed.</span></span>
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. <span data-ttu-id="acb5e-142">Теперь мы добрались до основной части нашей программы — мы будем запускать другие функции в зависимости от того, какие параметры были переданы.</span><span class="sxs-lookup"><span data-stu-id="acb5e-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. <span data-ttu-id="acb5e-143">Также мы будем проверять, передано ли нужное число параметров; если параметры имеют неправильный формат, будут отображены подсказки.</span><span class="sxs-lookup"><span data-stu-id="acb5e-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="acb5e-144">Давайте создадим для этого функции.</span><span class="sxs-lookup"><span data-stu-id="acb5e-144">Let's create functions to do that.</span></span>
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. <span data-ttu-id="acb5e-145">Кроме того, мы будем использовать на клиенте управления CDN асинхронные функции, поэтому нам нужен метод для обратного вызова после завершения их работы.</span><span class="sxs-lookup"><span data-stu-id="acb5e-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="acb5e-146">Давайте создадим такой метод, который будет отображать данные, полученные от клиента управления CDN (если они есть) и корректно завершать работу программы.</span><span class="sxs-lookup"><span data-stu-id="acb5e-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

<span data-ttu-id="acb5e-147">Теперь базовая структура программы полностью готова, и мы можем создать функции, вызываемые на основе полученных параметров.</span><span class="sxs-lookup"><span data-stu-id="acb5e-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="acb5e-148">Вывод списка профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="acb5e-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="acb5e-149">Давайте начнем с кода, который выводит список существующих профилей и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="acb5e-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="acb5e-150">Я дополню код комментариями с описанием синтаксиса, чтобы было понятно, для чего предназначен каждый параметр.</span><span class="sxs-lookup"><span data-stu-id="acb5e-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="acb5e-151">Создание профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="acb5e-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="acb5e-152">Теперь давайте напишем функцию для создания профилей и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="acb5e-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a><span data-ttu-id="acb5e-153">Очистка конечной точки</span><span class="sxs-lookup"><span data-stu-id="acb5e-153">Purge an endpoint</span></span>
<span data-ttu-id="acb5e-154">Одной из задач, которая может выполняться в программе после создания конечной точки, является очистка содержимого в ней.</span><span class="sxs-lookup"><span data-stu-id="acb5e-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="acb5e-155">Удаление профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="acb5e-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="acb5e-156">Наша последняя функция будет удалять конечные точки и профили.</span><span class="sxs-lookup"><span data-stu-id="acb5e-156">The last function we will include deletes endpoints and profiles.</span></span>

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-the-program"></a><span data-ttu-id="acb5e-157">Запуск программы</span><span class="sxs-lookup"><span data-stu-id="acb5e-157">Running the program</span></span>
<span data-ttu-id="acb5e-158">Теперь мы можем выполнить нашу программу Node.js в любом удобном отладчике или консоли.</span><span class="sxs-lookup"><span data-stu-id="acb5e-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> <span data-ttu-id="acb5e-159">Если вы используете в качестве отладчика Visual Studio Code, вам потребуется настроить среду для передачи параметров командной строки.</span><span class="sxs-lookup"><span data-stu-id="acb5e-159">If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.</span></span>  <span data-ttu-id="acb5e-160">Для этой цели в Visual Studio Code используется файл **lanuch.json** .</span><span class="sxs-lookup"><span data-stu-id="acb5e-160">Visual Studio Code does this in the **lanuch.json** file.</span></span>  <span data-ttu-id="acb5e-161">Найдите в нем свойство **args** и добавьте массив строковых значений со своими параметрами следующего вида: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="acb5e-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="acb5e-162">Давайте начнем с получения списка профилей.</span><span class="sxs-lookup"><span data-stu-id="acb5e-162">Let's start by listing our profiles.</span></span>

![Список профилей](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="acb5e-164">Мы получили пустой массив.</span><span class="sxs-lookup"><span data-stu-id="acb5e-164">We got back an empty array.</span></span>  <span data-ttu-id="acb5e-165">Так и должно быть, ведь в нашей группе ресурсов пока нет профилей.</span><span class="sxs-lookup"><span data-stu-id="acb5e-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="acb5e-166">Теперь давайте создадим профиль.</span><span class="sxs-lookup"><span data-stu-id="acb5e-166">Let's create a profile now.</span></span>

![Создание профиля](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="acb5e-168">Теперь мы добавим конечную точку.</span><span class="sxs-lookup"><span data-stu-id="acb5e-168">Now, let's add an endpoint.</span></span>

![Создать конечную точку](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="acb5e-170">И в завершение давайте удалим профиль.</span><span class="sxs-lookup"><span data-stu-id="acb5e-170">Finally, let's delete our profile.</span></span>

![Удаление профиля](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="acb5e-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="acb5e-172">Next Steps</span></span>
<span data-ttu-id="acb5e-173">Чтобы просмотреть описываемый в этом руководстве готовый проект, [скачайте пример](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="acb5e-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="acb5e-174">Справочную информацию о пакете SDK Azure CDN для Node.js вы найдете [здесь](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="acb5e-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="acb5e-175">Чтобы получить дополнительную документацию о пакете SDK Azure для Node.js, откройте [полный справочник](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="acb5e-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="acb5e-176">Управление ресурсами CDN с помощью [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="acb5e-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

