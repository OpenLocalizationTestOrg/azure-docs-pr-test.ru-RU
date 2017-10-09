---
title: "aaaCreate СРЕДНИМ стека на виртуальной Машине Linux в Azure | Документы Microsoft"
description: "Узнайте, как стека toocreate MongoDB, экспресс-выпуск, AngularJS и Node.js (среднее) на виртуальной Машине Linux в Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="a21ee-103">Создание стеков (MEAN) MongoDB, Express, AngularJS и Node.js на виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="a21ee-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="a21ee-104">Этот учебник показывает, как стека tooimplement MongoDB, экспресс-выпуск, AngularJS и Node.js (среднее) на виртуальной Машине Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="a21ee-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="a21ee-105">Hello среднее стека, который вы создаете включает добавление, удаление и список книг в базе данных.</span><span class="sxs-lookup"><span data-stu-id="a21ee-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="a21ee-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a21ee-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a21ee-107">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="a21ee-107">Create a Linux VM</span></span>
> * <span data-ttu-id="a21ee-108">Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="a21ee-108">Install Node.js</span></span>
> * <span data-ttu-id="a21ee-109">Установка MongoDB и настройка сервера hello</span><span class="sxs-lookup"><span data-stu-id="a21ee-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="a21ee-110">Установка экспресс-выпуск и настройка сервера toohello маршрутов</span><span class="sxs-lookup"><span data-stu-id="a21ee-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="a21ee-111">Маршруты hello доступа с помощью AngularJS</span><span class="sxs-lookup"><span data-stu-id="a21ee-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="a21ee-112">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="a21ee-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a21ee-113">Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="a21ee-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a21ee-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a21ee-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a21ee-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="a21ee-116">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="a21ee-116">Create a Linux VM</span></span>

<span data-ttu-id="a21ee-117">Создание группы ресурсов с hello [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) команды и создание виртуальной Машины Linux с hello [создания виртуальной машины az](https://docs.microsoft.com/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="a21ee-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="a21ee-118">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="a21ee-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="a21ee-119">Hello следующий пример использует hello Azure CLI toocreate группу ресурсов с именем *myResourceGroupMEAN* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="a21ee-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="a21ee-120">Создается виртуальная машина с именем *myVM* с ключами SSH, если они не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a21ee-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="a21ee-121">toouse определенный набор ключей, используйте hello--ssh ключ значение параметра.</span><span class="sxs-lookup"><span data-stu-id="a21ee-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

<span data-ttu-id="a21ee-122">При создании виртуальной Машины hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="a21ee-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
<span data-ttu-id="a21ee-123">Запишите hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="a21ee-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="a21ee-124">Этот адрес будет hello используется tooaccess виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a21ee-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="a21ee-125">Используйте hello следующая команда toocreate сеанс SSH с hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a21ee-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="a21ee-126">Убедитесь, что toouse hello открытый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a21ee-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="a21ee-127">В примере выше виртуальная машина имела следующий IP-адрес: 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="a21ee-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="a21ee-128">Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="a21ee-128">Install Node.js</span></span>

<span data-ttu-id="a21ee-129">[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript на базе ядра JavaScript Chrome V8.</span><span class="sxs-lookup"><span data-stu-id="a21ee-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="a21ee-130">В этот учебник tooset приветствия направляет Express, а контроллеры AngularJS используется node.js.</span><span class="sxs-lookup"><span data-stu-id="a21ee-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="a21ee-131">Установите на виртуальную Машину, с помощью команд bash hello, открытой с SSH, hello Node.js.</span><span class="sxs-lookup"><span data-stu-id="a21ee-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="a21ee-132">Установка MongoDB и настройка сервера hello</span><span class="sxs-lookup"><span data-stu-id="a21ee-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="a21ee-133">[MongoDB](http://www.mongodb.com) хранит данные в гибких документах, похожих на JSON-файлы.</span><span class="sxs-lookup"><span data-stu-id="a21ee-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="a21ee-134">Поля в базе данных может отличаться от toodocument документа и структуры данных может изменяться со временем.</span><span class="sxs-lookup"><span data-stu-id="a21ee-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="a21ee-135">Для нашего примера приложения мы добавляем tooMongoDB записи книги, содержащие имя книги, номер isbn, автор и количество страниц.</span><span class="sxs-lookup"><span data-stu-id="a21ee-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="a21ee-136">На hello виртуальную Машину, с помощью команд bash hello, открытой с SSH задайте ключ MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="a21ee-137">Обновление диспетчера пакетов hello с ключом hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="a21ee-138">Установите MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a21ee-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="a21ee-139">Запустите сервер hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="a21ee-140">Также нужны tooinstall hello [синтаксического анализа текста](https://www.npmjs.com/package/body-parser-json) пакета toohelp нам обработать hello JSON переданный server toohello запросов.</span><span class="sxs-lookup"><span data-stu-id="a21ee-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="a21ee-141">Установка диспетчера пакетов npm hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="a21ee-142">Установите пакет синтаксического анализа текста hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="a21ee-143">Создайте папку с именем *электронной* и добавьте tooit файл с именем *server.js* , содержащий конфигурацию hello hello веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="a21ee-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="a21ee-144">Установка экспресс-выпуск и настройка сервера toohello маршрутов</span><span class="sxs-lookup"><span data-stu-id="a21ee-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="a21ee-145">[Express](https://expressjs.com) — это небольшая гибкая платформа веб-приложений Node.js, которая предоставляет функции для веб-приложений и мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="a21ee-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="a21ee-146">Express используется в этой книги для учебника toopass сведения tooand из наших базы данных MongoDB.</span><span class="sxs-lookup"><span data-stu-id="a21ee-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="a21ee-147">[Mongoose](http://mongoosejs.com) предоставляет toomodel последовательных решение схемы данных приложения.</span><span class="sxs-lookup"><span data-stu-id="a21ee-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="a21ee-148">В этот учебник tooprovide используется mongoose книги схемы для базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="a21ee-149">Установите Express и Mongoose.</span><span class="sxs-lookup"><span data-stu-id="a21ee-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="a21ee-150">В hello *электронной* папки, создайте папку с именем *приложения* и добавьте в файл с именем *routes.js* с hello express маршрутов, указанных.</span><span class="sxs-lookup"><span data-stu-id="a21ee-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. <span data-ttu-id="a21ee-151">В hello *приложения* папки, создайте папку с именем *моделей* и добавьте в файл с именем *book.js* с определенные настройки модели книги hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="a21ee-152">Маршруты hello доступа с помощью AngularJS</span><span class="sxs-lookup"><span data-stu-id="a21ee-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="a21ee-153">[AngularJS](https://angularjs.org) представляет собой веб-платформу для создания динамических представлений в веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="a21ee-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="a21ee-154">В этом учебнике мы использовать AngularJS tooconnect наш веб-страницы с экспресс-выпуск и выполнять действия в базе данных книги.</span><span class="sxs-lookup"><span data-stu-id="a21ee-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="a21ee-155">Измените каталог hello резервное копирование слишком*электронной* (`cd ../..`) и создайте папку с именем *открытый* и добавьте в файл с именем *script.js* с контроллером hello определенные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a21ee-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. <span data-ttu-id="a21ee-156">В hello *открытый* папки, создайте файл с именем *index.html* с веб-страницы приветствия определен.</span><span class="sxs-lookup"><span data-stu-id="a21ee-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a><span data-ttu-id="a21ee-157">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="a21ee-157">Run hello application</span></span>

1. <span data-ttu-id="a21ee-158">Измените каталог hello резервное копирование слишком*электронной* (`cd ..`) и запустить сервер hello, запустив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a21ee-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="a21ee-159">Откройте веб-браузер toohello адрес, записанные для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a21ee-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="a21ee-160">Например, *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="a21ee-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="a21ee-161">Вы увидите примерно следующие страницы приветствия:</span><span class="sxs-lookup"><span data-stu-id="a21ee-161">You should see something like hello following page:</span></span>

    ![Запись о книге](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="a21ee-163">Введите данные в текстовых полях hello и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="a21ee-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="a21ee-164">Например:</span><span class="sxs-lookup"><span data-stu-id="a21ee-164">For example:</span></span>

    ![Добавление записи о книге](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="a21ee-166">После обновления страницы приветствия, вы увидите нечто похожее на этой странице:</span><span class="sxs-lookup"><span data-stu-id="a21ee-166">After refreshing hello page, you should see something like this page:</span></span>

    ![Список записей о книгах](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="a21ee-168">Можно щелкнуть **удаление** и удалить hello загрузочную запись из базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="a21ee-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a21ee-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a21ee-169">Next steps</span></span>

<span data-ttu-id="a21ee-170">В рамках этого руководства вы создали веб-приложение, отслеживающее записи о книгах, с помощью стека MEAN на виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="a21ee-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="a21ee-171">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a21ee-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a21ee-172">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="a21ee-172">Create a Linux VM</span></span>
> * <span data-ttu-id="a21ee-173">Установка Node.js</span><span class="sxs-lookup"><span data-stu-id="a21ee-173">Install Node.js</span></span>
> * <span data-ttu-id="a21ee-174">Установка MongoDB и настройка сервера hello</span><span class="sxs-lookup"><span data-stu-id="a21ee-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="a21ee-175">Установка экспресс-выпуск и настройка сервера toohello маршрутов</span><span class="sxs-lookup"><span data-stu-id="a21ee-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="a21ee-176">Маршруты hello доступа с помощью AngularJS</span><span class="sxs-lookup"><span data-stu-id="a21ee-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="a21ee-177">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="a21ee-177">Run hello application</span></span>

<span data-ttu-id="a21ee-178">Как переместить следующий учебник toolearn toohello toosecure веб-серверов с использованием сертификата SSL.</span><span class="sxs-lookup"><span data-stu-id="a21ee-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="a21ee-179">[Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)</span><span class="sxs-lookup"><span data-stu-id="a21ee-179">[Secure web server with SSL](tutorial-secure-web-server.md)</span></span>
