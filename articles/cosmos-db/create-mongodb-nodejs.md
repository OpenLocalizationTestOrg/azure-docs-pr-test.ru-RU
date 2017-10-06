---
title: "aaaConnect tooAzure приложения MongoDB Cosmos DB с помощью Node.js | Документы Microsoft"
description: "Узнайте, как tooconnect существующих приложений Node.js MongoDB tooAzure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a>Azure Cosmos DB. Перемещение имеющегося веб-приложения MongoDB Node.js 

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

Краткого руководства показано, как существующий toouse [MongoDB](mongodb-introduction.md) приложения, написанные на Node.js и подключите базу данных Azure Cosmos tooyour базы данных, которая поддерживает MongoDB клиентских подключений. Другими словами приложение Node.js знает только подключение tooa базы данных с помощью интерфейсов API MongoDB. Он является прозрачным toohello приложение, которое hello данных хранится в Azure Cosmos DB.

После выполнения шагов, описанных в этом руководстве, у вас будет приложение MEAN (MongoDB, Express, AngularJS и Node.js), выполняющееся в [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). 

![Приложение MEAN.js, которое запущено в службе приложений Azure](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, в этом разделе требуется под управлением hello Azure CLI версии 2.0 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="prerequisites"></a>Предварительные требования 
В дополнение к этому tooAzure CLI требуется [Node.js](https://nodejs.org/) и [Git](http://www.git-scm.com/downloads) установлены локально toorun `npm` и `git` команд.

У вас должен быть опыт работы с Node.js. Это краткое руководство не предназначено предполагаемого toohelp вы разработка приложений Node.js в целом.

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.  

Выполните следующие команды tooclone hello образец репозитория hello. Этот образец репозиторий содержит по умолчанию hello [MEAN.js](http://meanjs.org/) приложения. 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a>Запустите приложение hello

Установка hello необходимые пакеты и запуск приложения hello.

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a>Войдите в tooAzure

При использовании установленных Azure CLI вход tooyour подписки Azure с hello [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям. Этот шаг можно пропустить, если вы используете hello оболочки облако Azure.

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a>Добавить модуль Azure Cosmos DB hello

Если вы используете установленных Azure CLI, проверьте toosee, если hello `cosmosdb` компонент уже установлен, выполнив hello `az` команды. Если `cosmosdb` — в hello список базовых команд, продолжить toohello следующей команды. Этот шаг можно пропустить, если вы используете hello оболочки облако Azure.

Если `cosmosdb` не в hello список базовых команд, переустановите [Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание [группы ресурсов](../azure-resource-manager/resource-group-overview.md) с hello [Создание группы az](/cli/azure/group#create). Группа ресурсов Azure — это логический контейнер, в котором происходит развертывание ресурсов Azure (веб-приложений, баз данных и учетных записей хранения) и управление ими. 

Hello следующий пример создает группу ресурсов в Западной Европе hello. Выберите уникальное имя для группы ресурсов hello.

При использовании оболочки облако Azure щелкните **попробовать**, выполните toologin указаниям, появляющимся на экране приветствия, а затем скопируйте hello команду в командную строку hello.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a>создание учетной записи Azure Cosmos DB;

Создать учетную запись Azure Cosmos DB с hello [az cosmosdb создать](/cli/azure/cosmosdb#create) команды.

В hello выполните следующую команду, заменить собственные уникальное имя учетной записи Azure Cosmos DB, показывающий hello `<cosmosdb-name>` заполнителя. Это уникальное имя будет использоваться как часть конечной точки Azure Cosmos DB (`https://<cosmosdb-name>.documents.azure.com/`), поэтому hello имя должно toobe уникальным для всех учетных записей Azure Cosmos DB в Azure. 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

Hello `--kind MongoDB` обеспечивает MongoDB клиентских подключений.

При создании учетной записи Azure Cosmos DB hello hello Azure CLI показано toohello аналогичные сведения, следующий пример. 

> [!NOTE]
> В этом примере JSON как формат вывода hello Azure CLI, он по умолчанию hello. toouse другой выходной формат см. в разделе [выходных форматов для команд CLI Azure 2.0](https://docs.microsoft.com/cli/azure/format-output-azure-cli).

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a>Подключение базы данных приложения toohello Node.js

На этом шаге подключиться MEAN.js образец приложения tooan Azure Cosmos DB базы данных только что созданный, используя строку подключения MongoDB. 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Настройка строки подключения hello в приложении Node.js

В репозитории MEAN.js откройте `config/env/local-development.js`.

Замените содержимое этого файла hello hello, следующий код. Убедитесь, что tooalso замените hello двух `<cosmosdb-name>` местозаполнителей Azure Cosmos DB имя учетной записи.

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a>Получить ключ hello

В базе данных Azure Cosmos DB tooan tooconnect заказа необходим ключ hello базы данных. Используйте hello [список ключей az cosmosdb](/cli/azure/cosmosdb#list-keys) команда tooretrieve hello первичный ключ.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

Hello Azure CLI выводит toohello аналогичные сведения, следующий пример. 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

Скопируйте значение hello `primaryMasterKey`. Вставить это над hello `<primary_master_key>` в `local-development.js`.

Сохраните изменения.

### <a name="run-hello-application-again"></a>Запустите приложение hello еще раз.

Еще раз запустите `npm start`. 

```bash
npm start
```

Сообщения консоли теперь должен сообщить вам что этой среды разработки hello запущен и работает. 

Перейдите в слишком`http://localhost:3000` в браузере. Нажмите кнопку **зарегистрироваться** в верхнем меню и попробуйте toocreate hello два пустой пользователей. 

MEAN.js пример приложения Hello хранятся данные пользователя в базе данных hello. Если вы успешно и MEAN.js автоматически входит в hello создан пользователем, а затем подключение к базе данных Azure Cosmos работает. 

![MEAN.js успешно подключается tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a>Просмотр данных в обозревателе данных

Данные, хранящиеся в Azure Cosmos DB включена доступных tooview, запроса и выполнения бизнес логики в hello портал Azure.

tooview, запрос и работать с данными пользователя hello на предыдущем шаге hello, toohello входа [портал Azure](https://portal.azure.com) в веб-браузере.

В верхнем поле поиска hello введите Azure Cosmos DB. Когда откроется колонка учетной записи Cosmos DB, выберите свою учетную запись Cosmos DB. В hello навигации слева выберите обозреватель данных. Разверните коллекции в области коллекций hello и затем можно просматривать документы hello в коллекции hello, запроса данных hello и даже создать и выполнить хранимые процедуры, триггеры и определяемые пользователем функции. 

![Обозреватель данных в hello портал Azure](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a>Развертывание приложения tooAzure hello Node.js

На этом шаге развертывания вашего tooAzure приложение Node.js подключен MongoDB Cosmos DB.

Возможно, вы заметили это файл конфигурации hello ранее измененного для среды разработки hello (`/config/env/local-development.js`). При развертывании вашего приложения tooApp службы, он будет выполняться в hello рабочей среде по умолчанию. Поэтому теперь требуется toomake hello же изменить файл toohello соответствующей конфигурации.

В репозитории MEAN.js откройте `config/env/production.js`.

В hello `db` объекта, замените значение hello `uri` как показано в следующий пример hello. Быть убедиться, что заполнители hello tooreplace как до.

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> Hello `ssl=true` возможность важна поскольку [Azure Cosmos DB требуется протокол SSL](connect-mongodb-account.md#connection-string-requirements). 
>
>

В терминалов hello сохраните все изменения в Git. Обе команды toorun можно скопировать их вместе.

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, каким образом toocreate Cosmos Azure DB учетной записи и создать коллекцию MongoDB с использованием hello обозреватель данных. Теперь можно перенести на tooAzure данных MongoDB Cosmos DB.  

> [!div class="nextstepaction"]
> [Перенос данных в DocumentDB с помощью mongoimport и mongorestore](mongodb-migrate.md)
