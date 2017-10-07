---
title: "aaaGet работы с Azure ретрансляции гибридных подключений в .NET | Документы Microsoft"
description: "Написание консольного приложения #C для гибридных подключений ретранслятора Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Приступая к работе с гибридными подключениями к ретранслятору
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Этот учебник содержит введение слишком[гибридных подключений ретрансляции Azure](relay-what-is-it.md#hybrid-connections)и показано, как .NET toouse toocreate клиентское приложение, которое отправляет сообщения tooa соответствующее приложение прослушивателя. 

## <a name="what-will-be-accomplished"></a>Что будет выполнено
Так как гибридные подключения требуется клиентом и серверным компонентом, учебник hello создает два консольных приложений. Ниже приведены шаги hello.

1. Создание ретрансляции пространства имен, с помощью портала Azure hello.
2. Создайте гибридное подключение в этом пространстве имен, с помощью портала Azure hello.
3. Запись сообщений tooreceive приложения консоли сервера (прослушиватель).
4. Запись сообщений toosend приложения консоли клиента (отправителя).

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника вам потребуется hello следующие предварительные требования:

1. [Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com) Hello примерах в этом учебнике используется Visual Studio 2017 г.
2. Подписка Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Создание пространства имен с помощью портала Azure hello
Если вы уже создали имен ретрансляции, перехода toohello [создать гибридное подключение с помощью портала Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) раздела.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Создайте гибридное подключение с помощью портала Azure hello
Если вы уже создали гибридное подключение, перейдите к toohello [создать серверное приложение](#3-create-a-server-application-listener) раздела.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Создание серверного приложения (прослушивателя)
toolisten и получать сообщения из hello ретрансляции, мы напишем консольное приложение C# с помощью Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Создание клиентского приложения (отправителя)
Пересылать сообщения toohello toosend, мы напишем консольное приложение C# с помощью Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Запускать приложения hello
1. Запустите серверное приложение hello.
2. Запустите клиентское приложение hello и введите текст.
3. Убедитесь, что hello сервере приложения консоли выходы hello текст был введен в клиентском приложении hello.

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

Поздравляем, вы создали приложение для гибридных подключений.

## <a name="next-steps"></a>Дальнейшие действия:
* [Вопросы и ответы по ретранслятору](relay-faq.md)
* [Создание пространства имен](relay-create-namespace-portal.md)
* [Приступая к работе с Node](relay-hybrid-connections-node-get-started.md)

