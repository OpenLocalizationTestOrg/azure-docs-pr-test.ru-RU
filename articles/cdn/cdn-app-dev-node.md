---
title: "aaaGet работы с hello CDN Azure SDK для Node.js | Документы Microsoft"
description: "Узнайте, как toomanage приложений Node.js toowrite Azure CDN."
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
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="4c59e-103">Приступая к разработке для Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4c59e-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c59e-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="4c59e-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="4c59e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4c59e-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="4c59e-106">Можно использовать hello [Azure CDN SDK для Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate создания и управления профилями CDN и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="4c59e-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="4c59e-107">Этого учебника вы научитесь hello создание простой Node.js консольное приложение, которое показано несколько доступных операций hello.</span><span class="sxs-lookup"><span data-stu-id="4c59e-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="4c59e-108">Этот учебник является не предназначен toodescribe все аспекты hello CDN Azure SDK для Node.js подробно.</span><span class="sxs-lookup"><span data-stu-id="4c59e-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="4c59e-109">toocomplete этого учебника необходимо иметь [Node.js](http://www.nodejs.org) **4.х** или более поздней версии установлен и настроен.</span><span class="sxs-lookup"><span data-stu-id="4c59e-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="4c59e-110">Можно использовать любой текстовый редактор, требуется toocreate приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="4c59e-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="4c59e-111">toowrite этого учебника, я использовал [кода Visual Studio](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="4c59e-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="4c59e-112">Hello [завершенный проект из этого учебника](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) доступен для загрузки на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="4c59e-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="4c59e-113">Создание проекта и добавление зависимостей NPM</span><span class="sxs-lookup"><span data-stu-id="4c59e-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="4c59e-114">Теперь, что мы создали группу ресурсов для наших CDN профилей и заданным нашей профили CDN toomanage разрешений приложения Azure AD и конечных точек в пределах этой группы, можно начать создание нашего приложения.</span><span class="sxs-lookup"><span data-stu-id="4c59e-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="4c59e-115">Создайте toostore папку приложения.</span><span class="sxs-lookup"><span data-stu-id="4c59e-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="4c59e-116">В консоли с Node.js tools hello в текущем пути установить текущую папку новый toothis расположение и инициализировать проект, выполнив:</span><span class="sxs-lookup"><span data-stu-id="4c59e-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="4c59e-117">После этого будет представлен ряд вопросов tooinitialize проекта.</span><span class="sxs-lookup"><span data-stu-id="4c59e-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="4c59e-118">В качестве **точки входа**в этом руководстве используется *app.js*.</span><span class="sxs-lookup"><span data-stu-id="4c59e-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="4c59e-119">Вы увидите Мои другие варианты hello в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="4c59e-119">You can see my other choices in hello following example.</span></span>

![Выходные данные NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="4c59e-121">Теперь наш проект будет инициализирован с помощью файла *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="4c59e-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="4c59e-122">Наш проект будет toouse некоторые Azure библиотеки из пакета NPM.</span><span class="sxs-lookup"><span data-stu-id="4c59e-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="4c59e-123">Мы будем использовать hello среды выполнения клиента Azure для Node.js (ms rest azure) и hello клиентская библиотека CDN Azure для Node.js (azure arm cd).</span><span class="sxs-lookup"><span data-stu-id="4c59e-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="4c59e-124">Давайте добавим эти toohello проект как зависимости.</span><span class="sxs-lookup"><span data-stu-id="4c59e-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="4c59e-125">После этого пакеты hello установка, hello *package.json* файл должен выглядеть аналогичный пример toothis (версия цифры могут отличаться):</span><span class="sxs-lookup"><span data-stu-id="4c59e-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

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

<span data-ttu-id="4c59e-126">Наконец, используя текстовый редактор, создайте пустой текстовый файл и сохраните его в корне hello нашей папки проекта, как *в файле app.js*.</span><span class="sxs-lookup"><span data-stu-id="4c59e-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="4c59e-127">Теперь мы готовы toobegin написания кода.</span><span class="sxs-lookup"><span data-stu-id="4c59e-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="4c59e-128">Требования, константы, проверка подлинности и структура</span><span class="sxs-lookup"><span data-stu-id="4c59e-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="4c59e-129">С *в файле app.js* в наш редактор, приступим к базовой структуры нашей программы, написанной hello.</span><span class="sxs-lookup"><span data-stu-id="4c59e-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="4c59e-130">Добавьте hello» требует» для наших пакета NPM вверху hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="4c59e-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="4c59e-131">Мы должны toodefine некоторые константы, которые будут использовать наши методы.</span><span class="sxs-lookup"><span data-stu-id="4c59e-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="4c59e-132">Добавьте следующее hello.</span><span class="sxs-lookup"><span data-stu-id="4c59e-132">Add hello following.</span></span>  <span data-ttu-id="4c59e-133">Быть заполнители hello, включая hello убедиться, что tooreplace  **&lt;угловые скобки&gt;**, собственными значениями, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="4c59e-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="4c59e-134">Затем мы создать клиента управления CDN hello и присвойте ему нашей учетные данные.</span><span class="sxs-lookup"><span data-stu-id="4c59e-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="4c59e-135">Если вы используете аутентификацию отдельных пользователей, эти две строки будут выглядеть немного иначе.</span><span class="sxs-lookup"><span data-stu-id="4c59e-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4c59e-136">Этот пример кода следует используйте только при выборе toohave проверки подлинности пользователя вместо участника-службы.</span><span class="sxs-lookup"><span data-stu-id="4c59e-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="4c59e-137">Быть тщательно tooguard учетные данные пользователя и храните их в тайне.</span><span class="sxs-lookup"><span data-stu-id="4c59e-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="4c59e-138">Представлять tooreplace убедиться, что элементы hello в  **&lt;угловые скобки&gt;**  с hello исправить информацию.</span><span class="sxs-lookup"><span data-stu-id="4c59e-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="4c59e-139">Для `<redirect URI>`, использование перенаправления hello URI, введенное при регистрации приложения hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c59e-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="4c59e-140">Наш Node.js консольного приложения будет tootake некоторые параметры командной строки.</span><span class="sxs-lookup"><span data-stu-id="4c59e-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="4c59e-141">Давайте добавим проверку того, что передан хотя бы один параметр.</span><span class="sxs-lookup"><span data-stu-id="4c59e-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="4c59e-142">Мы заканчиваем toohello основную часть нашей программы, где мы ответвлениями tooother функции в зависимости от того, какие параметры были переданы.</span><span class="sxs-lookup"><span data-stu-id="4c59e-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="4c59e-143">В нескольких местах в нашей программе нам нужно убедиться, что были переданы в hello правильное количество параметров и отображения справки, если они выглядят правильно toomake.</span><span class="sxs-lookup"><span data-stu-id="4c59e-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="4c59e-144">Давайте создадим toodo функции.</span><span class="sxs-lookup"><span data-stu-id="4c59e-144">Let's create functions toodo that.</span></span>
   
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
7. <span data-ttu-id="4c59e-145">Наконец hello функций, которые мы будем использовать на клиенте управления CDN hello являются асинхронными, поэтому они должны toocall метод обратно в том случае, когда они все готово.</span><span class="sxs-lookup"><span data-stu-id="4c59e-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="4c59e-146">Сделаем, можно отобразить hello вывод hello CDN управления клиента (если таковые имеются) и корректно завершить работу программы hello.</span><span class="sxs-lookup"><span data-stu-id="4c59e-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
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

<span data-ttu-id="4c59e-147">Теперь, когда записывается hello базовой структуры программы, следует создавать hello функции на основе наших параметров.</span><span class="sxs-lookup"><span data-stu-id="4c59e-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="4c59e-148">Вывод списка профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="4c59e-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="4c59e-149">Начнем с кодом toolist наши существующие профили и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="4c59e-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="4c59e-150">Комментарии к коду предоставляют hello ожидается синтаксис, чтобы узнать, где каждый параметр становится.</span><span class="sxs-lookup"><span data-stu-id="4c59e-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="4c59e-151">Создание профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="4c59e-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="4c59e-152">Далее мы записываем профили toocreate функции hello и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="4c59e-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="4c59e-153">Очистка конечной точки</span><span class="sxs-lookup"><span data-stu-id="4c59e-153">Purge an endpoint</span></span>
<span data-ttu-id="4c59e-154">Предположим, что hello конечная точка создана, одной из общих задач, может потребоваться tooperform нашей программы удаления содержимого в конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4c59e-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="4c59e-155">Удаление профилей CDN и конечных точек</span><span class="sxs-lookup"><span data-stu-id="4c59e-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="4c59e-156">Hello последнюю функцию, которую будет реализована в удаляет конечные точки и профили.</span><span class="sxs-lookup"><span data-stu-id="4c59e-156">hello last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="4c59e-157">Запуск программы hello</span><span class="sxs-lookup"><span data-stu-id="4c59e-157">Running hello program</span></span>
<span data-ttu-id="4c59e-158">Теперь можно выполнить нашей программы Node.js с помощью наших любимых отладчика или с помощью консоли hello.</span><span class="sxs-lookup"><span data-stu-id="4c59e-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="4c59e-159">Если вы используете Visual Studio Code как отладчик, вам потребуется tooset копирование toopass вашей среды, параметры командной строки, hello.</span><span class="sxs-lookup"><span data-stu-id="4c59e-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="4c59e-160">Код Visual Studio для этого применяется hello **lanuch.json** файла.</span><span class="sxs-lookup"><span data-stu-id="4c59e-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="4c59e-161">Найдите свойство с именем **args** и добавить массив строковых значений параметров, таким образом, аналогичные toothis: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="4c59e-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="4c59e-162">Давайте начнем с получения списка профилей.</span><span class="sxs-lookup"><span data-stu-id="4c59e-162">Let's start by listing our profiles.</span></span>

![Список профилей](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="4c59e-164">Мы получили пустой массив.</span><span class="sxs-lookup"><span data-stu-id="4c59e-164">We got back an empty array.</span></span>  <span data-ttu-id="4c59e-165">Так и должно быть, ведь в нашей группе ресурсов пока нет профилей.</span><span class="sxs-lookup"><span data-stu-id="4c59e-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="4c59e-166">Теперь давайте создадим профиль.</span><span class="sxs-lookup"><span data-stu-id="4c59e-166">Let's create a profile now.</span></span>

![Создание профиля](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="4c59e-168">Теперь мы добавим конечную точку.</span><span class="sxs-lookup"><span data-stu-id="4c59e-168">Now, let's add an endpoint.</span></span>

![Создать конечную точку](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="4c59e-170">И в завершение давайте удалим профиль.</span><span class="sxs-lookup"><span data-stu-id="4c59e-170">Finally, let's delete our profile.</span></span>

![Удаление профиля](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="4c59e-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c59e-172">Next Steps</span></span>
<span data-ttu-id="4c59e-173">toosee hello завершения проекта из этого пошагового руководства [загрузить образец hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="4c59e-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="4c59e-174">Справочник hello toosee для hello Azure CDN SDK для Node.js hello представление [ссылка](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="4c59e-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="4c59e-175">дополнительную документацию по hello Azure SDK для Node.js hello представление toofind [полный Справочник по](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="4c59e-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="4c59e-176">Управление ресурсами CDN с помощью [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4c59e-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

