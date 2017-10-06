---
title: "Соединитель aaaDropbox в приложения логики Azure | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключите tooDropbox toomanage файлов. Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов в Dropbox."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a>Приступая к работе с Dropbox соединитель hello
Подключите tooDropbox toomanage файлов. Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов в Dropbox.

toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики. Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toodropbox"></a>Подключение tooDropbox
Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы. Таким образом вы установите соединение между приложением логики и другой службой. Например, в порядке tooconnect tooDropbox, необходимо сначала Dropbox *соединения*. toocreate соединение, потребовалось бы hello tooprovide учетные данные, обычно используемые службы hello tooaccess которых надо tooconnect для. Таким образом в примере hello общего банка данных, потребовалось бы tooyour hello учетные данные учетной записи общего банка данных в порядке toocreate hello соединения tooDropbox. Дополнительные сведения о подключениях см. [здесь]().

### <a name="create-a-connection-toodropbox"></a>Создание tooDropbox подключения
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a>Использование триггера Dropbox
Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики. [Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

В этом примере мы будем использовать hello **при создании файла** триггера. В случае триггера назовем hello **получить содержимое файла, используя путь** действие общего банка данных. 

1. Введите *dropbox* в поле поиска hello в конструкторе логики приложения hello, затем выберите hello **Dropbox - при создании файла** триггера.      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. Выберите папку hello, в котором tootrack создания файла. Выберите... (определенное в поле hello красный) и папки toohello обзора нужно входных tooselect для триггера hello.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a>Использование действия Dropbox
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Теперь, когда hello триггер был добавлен, выполните эти действия tooadd действия, которые помогут начать hello новый файл содержимого.

1. Выберите **+ новый шаг** действие hello tooadd хотелось бы tootake при создании нового файла.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. Выберите **Добавить действие**. Открывает окна поиска hello поиска для любого действия вы хотели бы tootake.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. Введите *dropbox* toosearch для tooDropbox связанные действия.  
4. Выберите **Dropbox - получение содержимого файла, используя путь** hello tootake действие создания нового файла в hello выбираются общего банка данных. Открывает блок управления действие Hello. Вам будет запрашиваемые tooauthorize вашей tooaccess логику приложения, учетной записи Dropbox, если вы еще не сделали это.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. Выберите... (расположенный в правой стороне hello hello **путь к файлу** управления) и найдите путь к файлу toohello хотелось бы toouse. Также можно использовать hello **путь к файлу** маркера toospeed вверх на создание логики приложения.  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. Сохраните данные и создать новый файл в общий банк данных tooactivate рабочего процесса.  

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/dropbox/).

## <a name="more-connectors"></a>Дополнительные сведения о соединителях
Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).
