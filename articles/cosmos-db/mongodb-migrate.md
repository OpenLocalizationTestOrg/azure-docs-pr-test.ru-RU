---
title: "aaaUse mongoimport и mongorestore с hello Azure Cosmos DB API для MongoDB | Документы Microsoft"
description: "Узнайте, как toouse mongoimport и mongorestore tooimport данные tooan API для MongoDB учетной записи"
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB: импорт данных MongoDB 

toomigrate данные из tooan MongoDB Azure Cosmos DB учетной записи для использования с hello API для MongoDB, необходимо выполнить следующее:

* Загрузите либо *mongoimport.exe* или *mongorestore.exe* из hello [центра загрузки MongoDB](https://www.mongodb.com/download-center).
* Получите [строку подключения API для MongoDB](connect-mongodb-account.md).

При импорте данных из toouse план и MongoDB с Здравствуйте, Azure Cosmos DB, следует использовать hello [средство переноса данных](import-data.md) tooimport данных.

В этом учебнике hello следующие задачи:

> [!div class="checklist"]
> * Получение строки подключения
> * Импорт данных MongoDB с помощью mongoimport
> * Импорт данных MongoDB с помощью mongorestore

## <a name="prerequisites"></a>Предварительные требования

* Увеличить пропускную способность: hello продолжительность переноса данных зависит от hello объем пропускной способности, настройка для коллекций. Быть убедиться, что пропускная способность hello tooincrease большего миграции данных. После завершения миграции hello уменьшения затрат toosave hello пропускной способности. Дополнительные сведения об увеличении пропускной способности в hello [портал Azure](https://portal.azure.com), в разделе [уровни производительности и ценовые категории в базе данных Azure Cosmos](performance-levels.md).

* Включите SSL. В Azure Cosmos DB строгие требования к безопасности и стандарты. Быть tooenable убедиться, что SSL при взаимодействии с вашей учетной записи. следующие процедуры Hello в hello оставшейся части статьи hello как tooenable SSL для mongoimport и mongorestore.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>Поиск сведений о строке подключения (узел, порт, имя пользователя и пароль)

1. В hello [портал Azure](https://portal.azure.com)в левой области hello, щелкнув hello **Azure Cosmos DB** входа.
2. В hello **подписки** области, выберите имя учетной записи.
3. В hello **строка подключения** колонка, щелкните **строка подключения**.  
Hello правой панели содержится вся информация hello, необходимость toosuccessfully подключения tooyour учетной записи.

    ![Колонка "Строка подключения"](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Импорт данных toohello API для MongoDB с помощью mongoimport

tooyour tooimport данных учетной записи Azure Cosmos DB, используйте следующий шаблон hello. Заполните *узла*, *username*, и *пароль* со значениями hello tooyour определенной учетной записи.  

Шаблон:

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

Пример:  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Импорт данных toohello API для MongoDB с помощью mongorestore

API tooyour toorestore данных MongoDB учетной записи, с помощью hello после импорта hello tooexecute шаблона. Заполните *узла*, *username*, и *пароль* со значениями hello tooyour определенной учетной записи.

Шаблон:

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

Пример:

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>Инструкции для успешного переноса

1. Заранее создайте и масштабируйте свои коллекции:
        
    * По умолчанию Azure Cosmos DB подготавливает новую коллекцию MongoDB, обеспечивающую пропускную способность 1000 единиц запроса в секунду (ЕЗ/с). Перед началом миграции hello с помощью mongoimport, mongorestore или mongomirror предварительно создать все коллекции из hello [портал Azure](https://portal.azure.com) или из средства и драйверы MongoDB. Если в коллекции больше, чем 10 ГБ, убедитесь, что toocreate [сегментированных и секционированные коллекции](partition-data.md) с ключом соответствующий сегмент.

    * Из hello [портал Azure](https://portal.azure.com), увеличить пропускную способность вашей коллекции из 1000 RUs для коллекции одну секцию и 2500 RUs для сегментированной коллекции только для миграции hello. С hello более высокую пропускную способность можно избежать регулирования и перенести за меньшее время. С ежечасное выставление счетов в базе данных Azure Cosmos, можно уменьшить пропускную способность hello сразу после hello миграции toosave затраты.

2. Вычислите hello приблизительное RU платы для записи одного документа.

    а. Подключите базы данных Azure Cosmos DB MongoDB tooyour hello MongoDB оболочки. Инструкции в [подключения tooAzure приложения MongoDB Cosmos DB](connect-mongodb-account.md).
    
    b. Выполните пример команды insert с помощью одного из документы образец hello MongoDB оболочки:
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. Выполните команду ```db.runCommand({getLastRequestStatistics: 1})```, в результате чего будет получен ответ, аналогичный этому:
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    d. Запишите hello запрос бесплатно.
    
3. Определение задержки hello из вашей машины toohello Azure Cosmos DB облачной службы:
    
    а. Включите подробное ведение журнала из hello MongoDB оболочки с помощью следующей команды:```setVerboseShell(true)```
    
    b. Выполнить простой запрос базы данных hello: ```db.coll.find().limit(1)```. В результате будет получен ответ, аналогичный этому:

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. Удаление документа hello вставлены до миграции tooensure hello, что нет повторяющихся документов. Для удаления документов можно использовать команду ```db.coll.remove({})```.

5. Вычислить приблизительное hello *batchSize* и *numInsertionWorkers* значения:

    * Для *batchSize*, деление hello всего подготовить RUs с RUs hello, взятые из записи в один документ на шаге 3.
    
    * Если учесть hello *batchSize* < = 24, использовать это число как ваш *batchSize* значение.
    
    * Если учесть hello *batchSize* > 24, набор hello *batchSize* too24 значение.
    
    * Для расчета *numInsertionWorkers* используйте следующую формулу: *numInsertionWorkers = (подготовленная пропускная способность * задержка в секундах) / (размер пакета * число ЕЗ, использованных для одной операции записи)*.
        
    |Свойство|Значение|
    |--------|-----|
    |batchSize| 24 |
    |Подготовленные ЕЗ | 10 000 |
    |Задержка | 0,100 с |
    |ЕЗ, использованные для записи 1 документа | 10 ЕЗ |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (10000 ЕЗ x 0,1 с) / (24 x 10 ЕЗ) = 4,1666*

6. Выполните команду hello окончательной миграции:

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>Дальнейшие действия

Можно продолжить toohello следующее руководство и узнайте, как tooquery данных MongoDB с использованием Azure Cosmos DB. 

> [!div class="nextstepaction"]
>[Как tooquery данных MongoDB?](../cosmos-db/tutorial-query-mongodb.md)
