---
title: "конечные точки REST aaaCall с HTTP + Swagger соединитель для приложения логики Azure | Документы Microsoft"
description: "Подключение tooREST конечных точек из приложения логики через Swagger hello HTTP + Swagger соединителя"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>Приступая к работе с hello HTTP + действие Swagger

Можно создать конечную точку REST tooany первого класса соединитель через [Swagger документа](https://swagger.io) при использовании hello HTTP + Swagger действия в рабочем процессе логику приложения. Кроме того, можно расширить toocall логику приложения любой конечной точки REST с эффективные возможности конструктора логики приложения.

статье toocreate логику приложения с помощью соединителей, toolearn [создайте новое приложение логики](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>Использование "HTTP + Swagger" в качестве триггера или действия

Здравствуйте HTTP + Swagger рабочих триггер и действие hello таким же как hello [действия HTTP](connectors-native-http.md) , но повышения удобства работы в конструкторе логики приложения, предоставляя hello API структуру и данные, возвращаемые hello [метаданных Swagger](https://swagger.io) . Здравствуйте, HTTP + Swagger соединитель также можно использовать как триггер. Tooimplement опроса триггер, выполните шаблон опроса hello, описанное в [создать пользовательский API-интерфейсы toocall другие интерфейсы API, служб и систем из приложения логики](../logic-apps/logic-apps-create-api-app.md#polling-triggers).

Дополнительные сведения о [триггерах и действиях приложения логики](connectors-overview.md).

Ниже приведен пример как toouse hello HTTP + Swagger операцию, так как действие рабочего процесса в приложении логику.

1. Выберите hello **новый шаг** кнопки.
2. Выберите **Добавить действие**.
3. Введите в поле поиска действие hello **swagger** toolist hello HTTP + Swagger действие.
   
    ![Выбор действия "HTTP + Swagger"](./media/connectors-native-http-swagger/using-action-1.png)
4. Тип hello URL-адрес для документа Swagger:
   
   * toowork из hello конструктор логики приложения, hello URL-адрес должен быть конечной точкой HTTPS и включен CORS.
   * Если документ Swagger hello не соответствует этим требованиям, можно использовать [хранилища Azure с CORS включен](#hosting-swagger-from-storage) toostore hello документа.
5. Нажмите кнопку **Далее** tooread и отрисовки из hello Swagger документа.
6. Добавьте параметры, необходимые для вызова hello HTTP.
   
    ![Выполнение действия HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave и опубликовать приложение логики, нажмите кнопку **Сохранить** на панели инструментов конструктора.

### <a name="host-swagger-from-azure-storage"></a>Размещение Swagger из службы хранилища Azure
Может потребоваться tooreference Swagger документа, не размещенного или, не соответствует требованиям безопасности и независимо от источника hello, для конструктора hello. tooresolve эту проблему, можно хранить hello Swagger документа в хранилище Azure и включить CORS tooreference hello документа.  

Ниже приведены шаги toocreate hello, настройте и хранения Swagger документы в хранилище Azure:

1. [Создайте учетную запись Azure с хранилищем BLOB-объектов Azure](../storage/common/storage-create-storage-account.md). tooperform это действие, задание разрешений слишком**общего доступа**.

2. Включите CORS hello большого двоичного объекта. 

   Этот параметр tooautomatically, можно использовать [этот сценарий PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).

3. Передача большого двоичного объекта файла Swagger toohello hello. 

   Этот этап можно выполнить из hello [портал Azure](https://portal.azure.com) или из такого средства, как [обозреватель хранилищ Azure](http://storageexplorer.com/).

4. Ссылаться на документ toohello ссылку HTTPS в хранилище больших двоичных объектов Azure. 

   ссылка Hello использует данный формат:

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>Технические сведения
Ниже приведены сведения hello для hello триггеров и действий, это HTTP + Swagger поддерживает соединитель.

## <a name="http--swagger-triggers"></a>Триггеры "HTTP + Swagger"
Триггер — это событие, которое может быть hello используется toostart рабочий процесс, который определен в приложение логики. [Дополнительные сведения о триггерах см. здесь.](connectors-overview.md) Здравствуйте HTTP + Swagger соединитель имеет один триггер.

| Триггер | Описание |
| --- | --- |
| HTTP + Swagger |Сделать вызов HTTP и возвращает содержимое ответа hello |

## <a name="http--swagger-actions"></a>Действия "HTTP + Swagger"
Действие — это операции, выполняемые hello рабочего процесса, определенные в приложение логики. [Дополнительные сведения о действиях см. здесь.](connectors-overview.md) Здравствуйте HTTP + Swagger соединитель имеет единственным возможным действием.

| Действие | Описание |
| --- | --- |
| HTTP + Swagger |Сделать вызов HTTP и возвращает содержимое ответа hello |

### <a name="action-details"></a>Сведения о действиях
Здравствуйте HTTP + Swagger соединитель поставляется с единственным возможным действием. Ниже приведены сведения о каждом из действия hello, обязательные и необязательные поля ввода и соответствующие сведения о выходных данных, связанных с их использованием hello.

#### <a name="http--swagger"></a>HTTP + Swagger
Выполните исходящий HTTP-запрос, используя метаданные Swagger.
Звездочка (*) означает, что поле является обязательным.

| Отображаемое имя | Имя свойства | Описание |
| --- | --- | --- |
| Метод* |метод |Toouse команд HTTP. |
| URI* |uri |URI для hello HTTP-запроса. |
| Заголовки |headers |Объект JSON tooinclude заголовков HTTP. |
| Текст |текст |Здравствуйте, HTTP-запроса. |
| Аутентификация |authentication |Toouse проверки подлинности для запроса. Дополнительные сведения см. в разделе hello [соединителя HTTP](connectors-native-http.md#authentication). |

**Сведения о выходных данных**

Ответ HTTP

| Имя свойства | Тип данных | Описание |
| --- | --- | --- |
| Заголовки |object |Заголовки ответов |
| Текст |object |Объект ответа |
| Код состояния |int |HTTP status code (Код состояния HTTP) |

### <a name="http-responses"></a>Ответы HTTP
При выполнении действия toovarious вызовов, можно получить определенные ответы. В таблице ниже приведены соответствующие ответы и описания.

| Name (Имя) | Описание |
| --- | --- |
| 200 |ОК |
| 202 |Принято |
| 400 |Недопустимый запрос |
| 401 |Не авторизовано |
| 403 |Запрещено |
| 404 |Не найдено |
| 500 |Внутренняя ошибка сервера. Произошла неизвестная ошибка. |

- - -
## <a name="next-steps"></a>Дальнейшие действия

* [Создайте приложение логики](../logic-apps/logic-apps-create-a-logic-app.md)
* [Список соединителей](apis-list.md)