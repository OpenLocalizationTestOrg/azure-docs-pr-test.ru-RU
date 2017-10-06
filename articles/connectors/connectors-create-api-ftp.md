---
title: "aaaLearn как toouse hello соединителя FTP в приложениях для логики | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключите toomanage сервера tooFTP файлов. Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов на FTP-сервере."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>Начало работы с соединителем hello FTP
Использовать соединитель toomonitor hello FTP, управлять и создания файлов с FTP-сервера. 

toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики. Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooftp"></a>Подключение tooFTP
Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы. Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.  

### <a name="create-a-connection-tooftp"></a>Создание tooFTP подключения
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>Использование триггера FTP
Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики. [Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!IMPORTANT]
> Hello FTP соединителя требуется FTP-сервер, который доступен из Интернета hello и настроен toooperate ПАССИВНЫЙ режим. Кроме того, соединитель hello FTP — **не совместим с неявное FTPS (FTP через SSL)**. Hello FTP connector поддерживает только явные FTPS (FTP через SSL).  
> 
> 

В этом примере будет показано как toouse hello **FTP - при добавлении или изменении файла** триггера tooinitiate логику приложения рабочего процесса, при добавлении файла, или изменена на FTP-сервере. В примере enterprise можно использовать этот триггер toomonitor FTP-папка для новых файлов, которые представляют заказы от клиентов.  Затем можно использовать действие соединителя FTP например **получение содержимого файла** tooget hello содержимое заказа hello для дальнейшей обработки и хранения в базе данных заказов.

1. Введите *ftp* в поле поиска hello в конструкторе приложений логики hello выберите hello **FTP - при добавлении или изменении файла** триггера   
   ![Изображение 1. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   Hello **при добавлении или изменении файла** открывает элемент управления  
   ![Изображение 2. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. Выберите hello **...**  на hello правой части элемента управления hello. Это открывает элемент управления для выбора папки hello  
   ![Изображение 3. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. Выберите hello  **>**  (стрелка вправо) и найдите папку hello toofind, чтобы получить toomonitor новые или измененные файлы. Выберите папку hello и обратите внимание, папка hello теперь отображается в hello **папки** элемента управления.  
   ![Изображение 4. Триггер FTP](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

На этом этапе приложение логики, были настроены триггер начала запуска hello других триггеров и действий в рабочем процессе hello при изменении или созданы в определенной папке FTP hello файла. 

> [!NOTE]
> Логика приложения toobe функциональной должен содержать хотя бы один триггер и одно действие. Следуйте указаниям hello hello Далее раздел tooadd действие.  
> 
> 

## <a name="use-a-ftp-action"></a>Использование действия FTP
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

Теперь, когда вы добавили триггер, выполните эти шаги tooadd действие, которое получит содержимое hello hello нового или измененного файла, найден триггером hello.    

1. Выберите **+ новый шаг** tooadd hello hello действие tooget hello содержимое hello файла на сервере hello FTP  
2. Выберите hello **добавить действие** ссылку.  
   ![Изображение 1. Действие FTP](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. Введите *FTP* toosearch для всех действий, связанных с tooFTP.
4. Выберите **FTP - получение содержимого файла** как hello tootake действие, если новый или измененный файл находится в папке hello FTP.      
   ![Изображение 2. Действие FTP](./media/connectors-create-api-ftp/ftp-action-2.png)  
   Hello **получение содержимого файла** управления откроется. **Примечание**: вы будет запрашиваемые tooauthorize вашей tooaccess логику приложения, на FTP-сервер учетную запись, если вы еще не сделали это.  
   ![Изображение 3. Действие FTP](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. Выберите hello **файл** управления (hello пробелы. он располагается ниже **ФАЙЛ***). Здесь можно использовать любой из hello различные свойства из hello нового или измененного файла, найден hello FTP-сервера.  
6. Выберите hello **содержимое файла** параметр.  
   ![Изображение 4. Действие FTP](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. обновлен элемент управления Hello, указывающее, что hello **FTP - получение содержимого файла** действие получит hello *содержимое файла* hello нового или измененного файла на сервере hello FTP.      
   ![Изображение 5. Действие FTP](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. Сохранить результаты работы, а затем добавить tootest папки FTP toohello файл рабочего процесса.    

На этом этапе приложение hello логику было настроено toomonitor триггер папку на FTP-сервер и инициировать hello рабочего процесса при обнаружении нового файла или открытии файла на сервере hello FTP. 

приложение Hello логику также настроен hello содержимое tooget действие hello нового или измененного файла.

Теперь можно добавить другое действие, например hello [SQL Server — вставить строку](connectors-create-api-sqlazure.md) содержимое hello tooinsert действие hello нового или измененного файла в таблицу базы данных SQL.  

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/ftpconnector/). 

## <a name="next-steps"></a>Дальнейшие действия
[Создайте приложение логики](../logic-apps/logic-apps-create-a-logic-app.md)

