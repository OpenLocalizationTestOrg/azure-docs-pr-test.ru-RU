---
title: "aaaLearn как toouse hello соединителя SFTP в приложениях для логики | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключите toosend tooSFTP API и получать файлы. Вы можете выполнять различные операции, например создавать, обновлять, получать или удалять файлы."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>Начало работы с соединителем SFTP hello
Используйте hello SFTP соединитель tooaccess toosend SFTP учетной записи и получать файлы. Вы можете выполнять различные операции, например создавать, обновлять, получать или удалять файлы.  

toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики. Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosftp"></a>Подключение tooSFTP
Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы. Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.  

### <a name="create-a-connection-toosftp"></a>Создание tooSFTP подключения
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>Использование триггера SFTP
Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики. [Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

В этом примере hello **SFTP - при добавлении или изменении файла** триггер является tooinitiate используется логика приложения рабочего процесса, при добавлении файла, или изменить на SFTP-сервере. Можно также добавить условие, которое проверяет содержимое hello hello нового или измененного файла и устанавливает файл hello tooextract принятия решений, если его содержимое указывает, должно быть извлечено перед использованием hello содержимое. Наконец добавьте действие tooextract hello содержимое файла и поместить в папку на SFTP-сервере hello hello извлечь содержимое. 

В пример enterprise можно использовать этот триггер toomonitor папки SFTP для новых файлов, которые представляют заказы клиента.  Затем можно использовать действие соединителя SFTP, таких как **получение содержимого файла**, содержимое hello tooget hello заказа для дальнейшей обработки и хранения в базе данных заказов.

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>Добавить условие
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>Использование действия SFTP
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/sftpconnector/).

## <a name="more-connectors"></a>Дополнительные сведения о соединителях
Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).
