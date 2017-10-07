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
# <a name="get-started-with-azure-cdn-development"></a>Приступая к разработке для Azure CDN
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Можно использовать hello [Azure CDN SDK для Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate создания и управления профилями CDN и конечных точек.  Этого учебника вы научитесь hello создание простой Node.js консольное приложение, которое показано несколько доступных операций hello.  Этот учебник является не предназначен toodescribe все аспекты hello CDN Azure SDK для Node.js подробно.

toocomplete этого учебника необходимо иметь [Node.js](http://www.nodejs.org) **4.х** или более поздней версии установлен и настроен.  Можно использовать любой текстовый редактор, требуется toocreate приложение Node.js.  toowrite этого учебника, я использовал [кода Visual Studio](https://code.visualstudio.com).  

> [!TIP]
> Hello [завершенный проект из этого учебника](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) доступен для загрузки на сайте MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>Создание проекта и добавление зависимостей NPM
Теперь, что мы создали группу ресурсов для наших CDN профилей и заданным нашей профили CDN toomanage разрешений приложения Azure AD и конечных точек в пределах этой группы, можно начать создание нашего приложения.

Создайте toostore папку приложения.  В консоли с Node.js tools hello в текущем пути установить текущую папку новый toothis расположение и инициализировать проект, выполнив:

    npm init

После этого будет представлен ряд вопросов tooinitialize проекта.  В качестве **точки входа**в этом руководстве используется *app.js*.  Вы увидите Мои другие варианты hello в следующем примере.

![Выходные данные NPM](./media/cdn-app-dev-node/cdn-npm-init.png)

Теперь наш проект будет инициализирован с помощью файла *packages.json* .  Наш проект будет toouse некоторые Azure библиотеки из пакета NPM.  Мы будем использовать hello среды выполнения клиента Azure для Node.js (ms rest azure) и hello клиентская библиотека CDN Azure для Node.js (azure arm cd).  Давайте добавим эти toohello проект как зависимости.

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

После этого пакеты hello установка, hello *package.json* файл должен выглядеть аналогичный пример toothis (версия цифры могут отличаться):

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

Наконец, используя текстовый редактор, создайте пустой текстовый файл и сохраните его в корне hello нашей папки проекта, как *в файле app.js*.  Теперь мы готовы toobegin написания кода.

## <a name="requires-constants-authentication-and-structure"></a>Требования, константы, проверка подлинности и структура
С *в файле app.js* в наш редактор, приступим к базовой структуры нашей программы, написанной hello.

1. Добавьте hello» требует» для наших пакета NPM вверху hello hello следующее:
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. Мы должны toodefine некоторые константы, которые будут использовать наши методы.  Добавьте следующее hello.  Быть заполнители hello, включая hello убедиться, что tooreplace  **&lt;угловые скобки&gt;**, собственными значениями, при необходимости.
   
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
3. Затем мы создать клиента управления CDN hello и присвойте ему нашей учетные данные.
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Если вы используете аутентификацию отдельных пользователей, эти две строки будут выглядеть немного иначе.
   
   > [!IMPORTANT]
   > Этот пример кода следует используйте только при выборе toohave проверки подлинности пользователя вместо участника-службы.  Быть тщательно tooguard учетные данные пользователя и храните их в тайне.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Представлять tooreplace убедиться, что элементы hello в  **&lt;угловые скобки&gt;**  с hello исправить информацию.  Для `<redirect URI>`, использование перенаправления hello URI, введенное при регистрации приложения hello в Azure AD.
4. Наш Node.js консольного приложения будет tootake некоторые параметры командной строки.  Давайте добавим проверку того, что передан хотя бы один параметр.
   
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
5. Мы заканчиваем toohello основную часть нашей программы, где мы ответвлениями tooother функции в зависимости от того, какие параметры были переданы.
   
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
6. В нескольких местах в нашей программе нам нужно убедиться, что были переданы в hello правильное количество параметров и отображения справки, если они выглядят правильно toomake.  Давайте создадим toodo функции.
   
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
7. Наконец hello функций, которые мы будем использовать на клиенте управления CDN hello являются асинхронными, поэтому они должны toocall метод обратно в том случае, когда они все готово.  Сделаем, можно отобразить hello вывод hello CDN управления клиента (если таковые имеются) и корректно завершить работу программы hello.
   
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

Теперь, когда записывается hello базовой структуры программы, следует создавать hello функции на основе наших параметров.

## <a name="list-cdn-profiles-and-endpoints"></a>Вывод списка профилей CDN и конечных точек
Начнем с кодом toolist наши существующие профили и конечных точек.  Комментарии к коду предоставляют hello ожидается синтаксис, чтобы узнать, где каждый параметр становится.

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

## <a name="create-cdn-profiles-and-endpoints"></a>Создание профилей CDN и конечных точек
Далее мы записываем профили toocreate функции hello и конечных точек.

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

## <a name="purge-an-endpoint"></a>Очистка конечной точки
Предположим, что hello конечная точка создана, одной из общих задач, может потребоваться tooperform нашей программы удаления содержимого в конечной точки.

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>Удаление профилей CDN и конечных точек
Hello последнюю функцию, которую будет реализована в удаляет конечные точки и профили.

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

## <a name="running-hello-program"></a>Запуск программы hello
Теперь можно выполнить нашей программы Node.js с помощью наших любимых отладчика или с помощью консоли hello.

> [!TIP]
> Если вы используете Visual Studio Code как отладчик, вам потребуется tooset копирование toopass вашей среды, параметры командной строки, hello.  Код Visual Studio для этого применяется hello **lanuch.json** файла.  Найдите свойство с именем **args** и добавить массив строковых значений параметров, таким образом, аналогичные toothis: `"args": ["list", "profiles"]`.
> 
> 

Давайте начнем с получения списка профилей.

![Список профилей](./media/cdn-app-dev-node/cdn-list-profiles.png)

Мы получили пустой массив.  Так и должно быть, ведь в нашей группе ресурсов пока нет профилей.  Теперь давайте создадим профиль.

![Создание профиля](./media/cdn-app-dev-node/cdn-create-profile.png)

Теперь мы добавим конечную точку.

![Создать конечную точку](./media/cdn-app-dev-node/cdn-create-endpoint.png)

И в завершение давайте удалим профиль.

![Удаление профиля](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>Дальнейшие действия
toosee hello завершения проекта из этого пошагового руководства [загрузить образец hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).

Справочник hello toosee для hello Azure CDN SDK для Node.js hello представление [ссылка](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).

дополнительную документацию по hello Azure SDK для Node.js hello представление toofind [полный Справочник по](http://azure.github.io/azure-sdk-for-node/).

Управление ресурсами CDN с помощью [PowerShell](cdn-manage-powershell.md).

