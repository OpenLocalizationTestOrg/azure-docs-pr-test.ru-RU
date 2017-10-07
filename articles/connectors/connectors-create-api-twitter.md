---
title: "aaaLearn как toouse hello соединителя Twitter в приложениях для логики | Документы Microsoft"
description: "Обзор соединителя Twitter с параметрами REST API"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8bce2183-544d-4668-a2dc-9a62c152d9fa
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: ead4e4dc95bf894fd72b908c5375b407ba27642d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twitter-connector"></a>Начало работы с соединителем hello Twitter
С помощью соединителя Twitter hello можно:

* публиковать и получать твиты;
* получать доступ к временным шкалам, просматривать друзей и подписчиков;
* Выполните любое из hello других действий и триггеров, описанные ниже  

toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики. Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).  

## <a name="connect-tootwitter"></a>Подключение tooTwitter
Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы. Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.  

### <a name="create-a-connection-tootwitter"></a>Создание tooTwitter подключения
> [!INCLUDE [Steps toocreate a connection tooTwitter](../../includes/connectors-create-api-twitter.md)]
> 
> 

## <a name="use-a-twitter-trigger"></a>Использование триггера Twitter
Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики. [Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

В этом примере будет показано как toouse hello **при учете новый твит** инициирует toosearch для #Seattle и, при обнаружении #Seattle обновления файла в общий банк данных с текстом hello твит hello. В примере enterprise может поиск hello название вашей компании и обновления базы данных SQL с текстом hello твит hello.

1. Введите *twitter* в поле поиска hello в конструкторе приложений логики hello выберите hello **Twitter - при публикации новых твит** триггера   
   ![Изображение 1. Триггер Twitter](./media/connectors-create-api-twitter/trigger-1.png)  
2. Введите *#Seattle* в hello **искомый текст** управления  
   ![Изображение 2. Триггер Twitter](./media/connectors-create-api-twitter/trigger-2.png) 

На этом этапе приложение логики, были настроены триггер начала запуска hello других триггеров и действий в рабочем процессе hello. 

> [!NOTE]
> Логика приложения toobe функциональной должен содержать хотя бы один триггер и одно действие. Следуйте указаниям hello hello Далее раздел tooadd действие.  
> 
> 

## <a name="add-a-condition"></a>Добавить условие
Так как нас интересуют только твиты у пользователей с более чем 50 пользователей, условие, которое подтверждает hello число последователи сначала необходимо добавить toohello логику приложения.  

1. Выберите **+ новый шаг** действие hello tooadd хотелось бы tootake при обнаружении нового твит #Seattle  
   ![Изображение 1. Действие Twitter](../../includes/media/connectors-create-api-twitter/action-1.png)  
2. Выберите hello **добавить условие** ссылку.  
   ![Изображение 1. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-1.png)   
   При этом откроется hello **условие** управления, где можно проверять условия, такие как *равен*, *— меньше, чем*, *больше, чем*, *содержит*и т. д.  
   ![Изображение 2. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-2.png)   
3. Выберите hello **выберите значение** элемента управления.  
   В этом элементе управления можно выбрать одно или несколько свойств hello из предыдущих действиях или триггеров как hello значение, которое будет вычисленное tootrue или false.
   ![Изображение 3. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-3.png)   
4. Выберите hello **...**  tooexpand hello список свойств, чтобы можно было видеть все доступные свойства hello.        
   ![Изображение 4. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-4.png)   
5. Выберите hello **число последователи** свойство.    
   ![Изображение 5. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-5.png)   
6. Обратите внимание, свойство count находится в элемент управления значения hello последователи hello.    
   ![Изображение 6: условие Twitter](../../includes/media/connectors-create-api-twitter/condition-6.png)   
7. Выберите **больше, чем** из списка операторов hello.    
   ![Изображение 7. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-7.png)   
8. Введите 50 как hello операнд для hello *больше, чем* оператор.  
   Теперь добавляется условие Hello. Сохраните данные с помощью hello **Сохранить** ссылку в меню "hello" выше.    
   ![Изображение 8. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-8.png)   

## <a name="use-a-twitter-action"></a>Использование действия Twitter
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Теперь, когда вы добавили триггер, выполните эти действия tooadd действия, которая получит новый твит hello содержимое твиты hello найден триггером hello. Для целей данного обучения hello будет учитываться только твиты у пользователей с более чем 50 последователи.  

В следующем шаге hello вы добавите Twitter действие, которое будет учитывать твит с помощью свойств каждого отправленного пользователем, который имеет более чем 50 последователи твит hello.  

1. Выберите **Добавить действие**. При этом откроется hello управления поиска, где можно найти другие действия и триггеры.  
   ![Изображение 9. Условие Twitter](../../includes/media/connectors-create-api-twitter/condition-9.png)   
2. Введите *twitter* в поле поиска hello выберите hello **Twitter - Post твит** действия. Откроется hello **Post твит** управления можно будет ввести все сведения для учитываемых твит hello.      
   ![Изображения 1–5. Действие Twitter](../../includes/media/connectors-create-api-twitter/action-1-5.png)   
3. Выберите hello **твит текст** элемента управления. Будут отображены все выходные данные предыдущих действий и триггеров в приложение логику hello. Можно выбрать любой из этих и использовать их как часть текст hello твит новый твит hello.     
   ![Действие Twitter, изображение 2](../../includes/media/connectors-create-api-twitter/action-2.png)   
4. Выберите **Имя пользователя**.   
5. Введите *говорит:* в элементе управления текст твит hello. Это фразу нужно ввести сразу после имени пользователя.  
6. Выберите *Tweet text* (Текст твита).       
   ![Действие Twitter, изображение 3](../../includes/media/connectors-create-api-twitter/action-3.png)   
7. Сохраните свою работу и отправки твитов с tooactivate хэштегом hello #Seattle рабочего процесса.  


## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/twitterconnector/). 

## <a name="next-steps"></a>Дальнейшие действия
[Создайте приложение логики](../logic-apps/logic-apps-create-a-logic-app.md)

