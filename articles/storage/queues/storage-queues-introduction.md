---
title: "aaaIntroduction tooAzure хранилища очередей | Документы Microsoft"
description: "Введение tooAzure хранилища очередей"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>Введение tooQueues

Хранилище Azure очереди — это служба для хранения большого количества сообщений, которые может осуществляться из любого места в Здравствуй, мир! через вызовы прошедшего проверку подлинности, протокол HTTP или HTTPS. Сообщение одной очереди может быть вверх too64 КБ и очередь может содержать миллионы сообщений вверх toohello предел общая емкость учетной записи хранения.

## <a name="common-uses"></a>Распространенные варианты использования

Наиболее частые способы использования хранилища очередей включают:

* Создание невыполненной работы tooprocess асинхронно
* Передача сообщений из Azure web роли tooan рабочей роли Azure

## <a name="queue-service-concepts"></a>Основные понятия службы очередей

Служба очередей Hello содержит hello следующие компоненты:

![Понятия очереди](./media/storage-queues-introduction/queue1.png)

* **Формат URL-адреса:** очереди можно с помощью hello следующий формат URL-адреса:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    URL-адреса Hello адреса очереди в диаграмме hello:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Учетная запись хранения:** обращаться к tooAzure хранилища осуществляется через учетную запись хранилища. Сведения об емкости учетной записи хранения см. в статье [Целевые показатели масштабируемости и производительности службы хранилища Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).

* **Очередь**. Очередь содержит набор сообщений. Все сообщения должны находиться в очереди. Обратите внимание, что это имя очереди hello должны указываться прописными буквами. Дополнительные сведения см. в статье о [присвоении имен очередям и метаданным](https://msdn.microsoft.com/library/azure/dd179349.aspx).

* **Сообщение об ошибке:** A-сообщения, в любом формате из копии too64 КБ. Максимальное время Hello, сообщение может оставаться в очереди hello составляет семь дней.

## <a name="next-steps"></a>Дальнейшие действия

* [создать учетную запись хранения;](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Начало работы с очередями с использованием .NET](storage-dotnet-how-to-use-queues.md)
