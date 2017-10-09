---
title: "aaaGet работы с Azure ретрансляции гибридных подключений в узле | Документы Microsoft"
description: "Написание консольного приложения Node.js для гибридных подключений ретранслятора Azure."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Приступая к работе с гибридными подключениями к ретранслятору

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Этот учебник содержит введение слишком[гибридных подключений ретрансляции Azure](relay-what-is-it.md#hybrid-connections)и показано, как toocreate Node.js toouse клиентское приложение, которое отправляет сообщения tooa соответствующее приложение прослушивателя. 

## <a name="what-will-be-accomplished"></a>Что будет выполнено

Так как для гибридных подключений требуется компонент клиента и сервера, в этом руководстве мы создадим два консольных приложения. Ниже приведены шаги hello.

1. Создание ретрансляции пространства имен, с помощью портала Azure hello.
2. Создайте гибридное подключение, с помощью портала Azure hello.
3. Запись сообщения tooreceive приложения консоли сервера.
4. Запись сообщений toosend консольного приложения клиента.

## <a name="prerequisites"></a>Предварительные требования

1. [Node.js](https://nodejs.org/en/).
2. Подписка Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Создание пространства имен с помощью портала Azure hello

При наличии ретрансляции пространство имен, созданное перехода toohello [создать гибридное подключение с помощью портала Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) раздела.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Создайте гибридное подключение с помощью портала Azure hello

Если уже создан гибридное подключение, перейдите к toohello [создать серверное приложение](#3-create-a-server-application-listener) раздела.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Создание серверного приложения (прослушивателя)

toolisten и получать сообщения от hello ретрансляции, мы напишем консольное приложение Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Создание клиентского приложения (отправителя)

toosend сообщений toohello ретрансляции, мы напишем консольное приложение Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Запускать приложения hello

1. Запустите серверное приложение hello: в командной строке введите Node.js `node listener.js`.
2. Запуск клиентского приложения hello: в командной строке введите Node.js `node sender.js`и введите любой текст.
3. Убедитесь, что hello сервере приложения консоли выходы hello текст был введен в клиентском приложении hello.

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Поздравляем, вы создали приложение для гибридных подключений с помощью Node.js!

## <a name="next-steps"></a>Дальнейшие действия:

* [Вопросы и ответы по ретранслятору](relay-faq.md)
* [Создание пространства имен](relay-create-namespace-portal.md)
* [Приступая к работе с .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Приступая к работе с Node](relay-hybrid-connections-node-get-started.md)

