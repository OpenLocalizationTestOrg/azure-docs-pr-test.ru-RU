---
title: "Настройка Postman для вызовов REST API служб мультимедиа Azure"
description: "Узнайте, как настроить Postman для вызовов REST API служб мультимедиа Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/04/2017
ms.author: juliako
ms.openlocfilehash: a24b73a93bddbeb5b56ddfdf604fa99faccea442
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="configure-postman-for-media-services-rest-api-calls"></a>Настройка Postman для вызовов REST API служб мультимедиа

В этом руководстве описано, как настроить **Postman** для вызова REST API служб мультимедиа Azure (AMS). В руководстве также показано, как импортировать файлы среды и коллекции в **Postman**. Коллекция содержит сгруппированные определения HTTP-запросов, которые вызывают REST API служб мультимедиа Azure (AMS). Файл среды содержит переменные, которые используются коллекцией.

Среда и коллекция описаны в руководствах по выполнению различных задач с помощью REST API служб мультимедиа Azure.

## <a name="prerequisites"></a>Необходимые компоненты

- Установите клиент REST [Postman](https://www.getpostman.com/) для выполнения REST API, как показано в некоторых руководствах по REST AMS. 

    Мы используем **Postman**, но подойдет любое средство REST. Другие варианты включают **Visual Studio Code** с подключаемым модулем REST или **Telerik Fiddler**. 

## <a name="configure-the-environment"></a>Настройка среды 

1. Создайте JSON-файл, содержащий переменные среды, используемые в руководствах по AMS. Назовите файл **AzureMediaServices.postman_environment.json**. Откройте файл и вставьте код, который определяет среду Postman из [этого примера кода](postman-environment.md). 
2. Откройте **Postman**.
3. В правой части экрана выберите параметр **Управление средой**.

    ![Отправить файл.](./media/media-services-rest-upload-files/postman-create-env.png)
4. В диалоговом окне **Управление средой** нажмите кнопку **Импорт**.
5. Найдите и выберите файл **AzureMediaServices.postman_environment.json**.
6. Будет добавлена среда **AzureMedia**.
7. Закройте диалоговое окно.
8. Выберите среду **AzureMedia**.

    ![Отправить файл.](./media/media-services-rest-upload-files/postman-choose-env.png)

## <a name="configure-the-collection"></a>Настройка коллекции

1. Создайте JSON-файл, содержащий коллекцию **Postman** со всеми операциями, которые необходимы для передачи файла в службы мультимедиа. Назовите файл **AzureMediaServicesOperations.postman_collection.json**. Откройте файл и вставьте код, который определяет коллекцию **Postman** из этого [примера кода](postman-collection.md).
2. Нажмите кнопку **импорта**, чтобы импортировать файл коллекции.
3. Выберите файл **AzureMediaServicesOperations.postman_collection.json**.

    ![Отправить файл.](./media/media-services-rest-upload-files/postman-import-collection.png)

## <a name="next-steps"></a>Дополнительная информация

См. руководство по [передаче файлов](media-services-rest-upload-files.md).  
