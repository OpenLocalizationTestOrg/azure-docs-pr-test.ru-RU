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
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>Создание стеков (MEAN) MongoDB, Express, AngularJS и Node.js на виртуальной машине Linux в Azure

Этот учебник показывает, как стека tooimplement MongoDB, экспресс-выпуск, AngularJS и Node.js (среднее) на виртуальной Машине Linux в Azure. Hello среднее стека, который вы создаете включает добавление, удаление и список книг в базе данных. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создание виртуальной машины Linux
> * Установка Node.js
> * Установка MongoDB и настройка сервера hello
> * Установка экспресс-выпуск и настройка сервера toohello маршрутов
> * Маршруты hello доступа с помощью AngularJS
> * Запустите приложение hello

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, упражнений этого учебника требуется, вы используете версию Azure CLI hello 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).


## <a name="create-a-linux-vm"></a>Создание виртуальной машины Linux

Создание группы ресурсов с hello [Создание группы az](https://docs.microsoft.com/cli/azure/group#create) команды и создание виртуальной Машины Linux с hello [создания виртуальной машины az](https://docs.microsoft.com/cli/azure/vm#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.

Hello следующий пример использует hello Azure CLI toocreate группу ресурсов с именем *myResourceGroupMEAN* в hello *eastus* расположение. Создается виртуальная машина с именем *myVM* с ключами SSH, если они не существуют в расположении ключей по умолчанию. toouse определенный набор ключей, используйте hello--ssh ключ значение параметра.

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

При создании виртуальной Машины hello hello Azure CLI показано toohello аналогичные сведения, следующий пример: 

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
Запишите hello `publicIpAddress`. Этот адрес будет hello используется tooaccess виртуальной Машины.

Используйте hello следующая команда toocreate сеанс SSH с hello виртуальной Машины. Убедитесь, что toouse hello открытый IP-адрес. В примере выше виртуальная машина имела следующий IP-адрес: 13.72.77.9.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Установка Node.js

[Node.js](https://nodejs.org/en/) — это среда выполнения JavaScript на базе ядра JavaScript Chrome V8. В этот учебник tooset приветствия направляет Express, а контроллеры AngularJS используется node.js.

Установите на виртуальную Машину, с помощью команд bash hello, открытой с SSH, hello Node.js.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>Установка MongoDB и настройка сервера hello
[MongoDB](http://www.mongodb.com) хранит данные в гибких документах, похожих на JSON-файлы. Поля в базе данных может отличаться от toodocument документа и структуры данных может изменяться со временем. Для нашего примера приложения мы добавляем tooMongoDB записи книги, содержащие имя книги, номер isbn, автор и количество страниц. 

1. На hello виртуальную Машину, с помощью команд bash hello, открытой с SSH задайте ключ MongoDB hello.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Обновление диспетчера пакетов hello с ключом hello.
  
    ```bash
    sudo apt-get update
    ```

3. Установите MongoDB.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Запустите сервер hello.

    ```bash
    sudo service mongodb start
    ```

5. Также нужны tooinstall hello [синтаксического анализа текста](https://www.npmjs.com/package/body-parser-json) пакета toohelp нам обработать hello JSON переданный server toohello запросов.

    Установка диспетчера пакетов npm hello.

    ```bash
    sudo apt-get install npm
    ```

    Установите пакет синтаксического анализа текста hello.
    
    ```bash
    sudo npm install body-parser
    ```

6. Создайте папку с именем *электронной* и добавьте tooit файл с именем *server.js* , содержащий конфигурацию hello hello веб-сервера.

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

## <a name="install-express-and-set-up-routes-toohello-server"></a>Установка экспресс-выпуск и настройка сервера toohello маршрутов

[Express](https://expressjs.com) — это небольшая гибкая платформа веб-приложений Node.js, которая предоставляет функции для веб-приложений и мобильных приложений. Express используется в этой книги для учебника toopass сведения tooand из наших базы данных MongoDB. [Mongoose](http://mongoosejs.com) предоставляет toomodel последовательных решение схемы данных приложения. В этот учебник tooprovide используется mongoose книги схемы для базы данных hello.

1. Установите Express и Mongoose.

    ```bash
    sudo npm install express mongoose
    ```

2. В hello *электронной* папки, создайте папку с именем *приложения* и добавьте в файл с именем *routes.js* с hello express маршрутов, указанных.

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

3. В hello *приложения* папки, создайте папку с именем *моделей* и добавьте в файл с именем *book.js* с определенные настройки модели книги hello.  

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

## <a name="access-hello-routes-with-angularjs"></a>Маршруты hello доступа с помощью AngularJS

[AngularJS](https://angularjs.org) представляет собой веб-платформу для создания динамических представлений в веб-приложениях. В этом учебнике мы использовать AngularJS tooconnect наш веб-страницы с экспресс-выпуск и выполнять действия в базе данных книги.

1. Измените каталог hello резервное копирование слишком*электронной* (`cd ../..`) и создайте папку с именем *открытый* и добавьте в файл с именем *script.js* с контроллером hello определенные конфигурации.

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
    
2. В hello *открытый* папки, создайте файл с именем *index.html* с веб-страницы приветствия определен.

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

##  <a name="run-hello-application"></a>Запустите приложение hello

1. Измените каталог hello резервное копирование слишком*электронной* (`cd ..`) и запустить сервер hello, запустив следующую команду:

    ```bash
    nodejs server.js
    ```

2. Откройте веб-браузер toohello адрес, записанные для hello виртуальной Машины. Например, *http://13.72.77.9:3300*. Вы увидите примерно следующие страницы приветствия:

    ![Запись о книге](media/tutorial-mean/meanstack-init.png)

3. Введите данные в текстовых полях hello и нажмите кнопку **добавить**. Например:

    ![Добавление записи о книге](media/tutorial-mean/meanstack-add.png)

4. После обновления страницы приветствия, вы увидите нечто похожее на этой странице:

    ![Список записей о книгах](media/tutorial-mean/meanstack-list.png)

5. Можно щелкнуть **удаление** и удалить hello загрузочную запись из базы данных hello.

## <a name="next-steps"></a>Дальнейшие действия

В рамках этого руководства вы создали веб-приложение, отслеживающее записи о книгах, с помощью стека MEAN на виртуальной машине Linux. Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * Создание виртуальной машины Linux
> * Установка Node.js
> * Установка MongoDB и настройка сервера hello
> * Установка экспресс-выпуск и настройка сервера toohello маршрутов
> * Маршруты hello доступа с помощью AngularJS
> * Запустите приложение hello

Как переместить следующий учебник toolearn toohello toosecure веб-серверов с использованием сертификата SSL.

> [!div class="nextstepaction"]
> [Secure a web server with SSL certificates on a Linux virtual machine in Azure](tutorial-secure-web-server.md) (Защита веб-сервера на виртуальной машине Linux в облаке Azure с помощью SSL-сертификата)
