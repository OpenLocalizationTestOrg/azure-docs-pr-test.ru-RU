---
title: "Строка подключения aaaMongoDB для учетной записи Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как tooconnect tooan приложения вашей MongoDB Azure Cosmos DB записи с помощью строки подключения MongoDB."
keywords: "строка подключения MongoDB"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>Подключение tooAzure приложения MongoDB Cosmos DB
Узнайте, как tooconnect tooan приложения вашей MongoDB Azure Cosmos DB записи с помощью строки подключения MongoDB. Затем можно использовать базу данных Azure Cosmos DB как hello данные хранилища для приложения MongoDB. 

Этот учебник предлагает два способа tooretrieve данные строки подключения:

- [метод start Hello быстрого](#QuickstartConnection), для использования с драйверами .NET, Node.js, MongoDB оболочки, Java и Python
- [Здравствуйте, метод строк пользовательского подключения](#GetCustomConnection), для использования с другими драйверами

## <a name="prerequisites"></a>Предварительные требования

- Учетная запись Azure. Если у вас нет учетной записи, вы можете создать [бесплатную учетную запись Azure](https://azure.microsoft.com/free/). 
- Учетная запись Azure Cosmos DB. Инструкции см. в разделе [построения MongoDB API веб-приложения с помощью .NET и hello портал Azure](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Получить строку подключения hello MongoDB с помощью быстрого запуска hello
1. В веб-браузере вход toohello [портал Azure](https://portal.azure.com).
2. В hello **Azure Cosmos DB** колонке выберите hello API для учетной записи MongoDB. 
3. Hello левой части колонки hello учетной записи, нажмите кнопку **краткого**. 
4. Выберите платформу (**.NET**, **Node.js**, **оболочка MongoDB**, **Java**, **Python**). Если соответствующего драйвера или средства нет в списке, не беспокойтесь, мы постоянно добавляем дополнительные фрагменты кода для подключения. Оставьте комментарий ниже на хотелось бы toosee. toolearn как toocraft подключения, считывать [получить строку подключения учетной записи hello](#GetCustomConnection).
5. Скопируйте и вставьте фрагмент кода hello в приложении MongoDB.

    ![Колонка "Быстрый запуск"](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Получить подключение строку hello MongoDB toocustomize
1. В веб-браузере вход toohello [портал Azure](https://portal.azure.com).
2. В hello **Azure Cosmos DB** колонке выберите hello API для учетной записи MongoDB. 
3. Hello левой части колонки hello учетной записи, нажмите кнопку **строка подключения**. 
4. Hello **строка подключения** открывает колонку. Он имеет все hello сведения о необходимости tooconnect toohello учетную запись с помощью драйвера для MongoDB, включая строку preconstructed подключения.

    ![Колонка "Строка подключения"](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Требования к строке подключения
> [!Important]
> В Azure Cosmos DB строгие требования к безопасности и стандарты. Для всех учетных записей Azure Cosmos DB требуется проверка подлинности и безопасный обмен данными через *SSL*. 
>
>

Azure Cosmos DB поддерживает hello Стандартная MongoDB формат строки подключения URI, с помощью нескольких конкретных требований: учетные записи Azure Cosmos DB требовать проверку подлинности и безопасного взаимодействия через SSL. Таким образом является формат строки соединения hello:

    mongodb://username:password@host:port/[database]?ssl=true

Hello значения этой строки доступны в hello **строка подключения** колонки, показанного выше:

* Имя пользователя (обязательно): имя учетной записи Azure Cosmos DB.
* Пароль (обязательно): пароль для учетной записи Azure Cosmos DB.
* Узел (обязательно): полное доменное имя учетной записи Azure Cosmos DB hello.
* Порт (обязательно): 10255.
* База данных (необязательно): hello базы данных, которая hello соединение использует. Если база данных не указан, база данных по умолчанию hello — «проверка».
* ssl=true (обязательно)

Допустим, учетная запись hello показано hello **строка подключения** колонку. Допустимая строка подключения:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[использовать MongoChef](mongodb-mongochef.md) Azure Cosmos DB API-интерфейсы для учетной записи MongoDB.
* Просмотр hello Azure Cosmos DB API для MongoDB, просмотрев [образцы](mongodb-samples.md).
