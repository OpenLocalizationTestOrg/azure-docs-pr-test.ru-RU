---
title: "aaaConnect tooan локальной системы SAP в Azure Logic Apps | Документы Microsoft"
description: "Подключение tooan в локальной системе SAP из рабочего процесса логику приложения через hello локального шлюза данных"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Подключение из логики приложений с помощью соединителя SAP hello tooan в локальной системе SAP 

Hello локального шлюза данных позволяет вам toomanage данных и безопасный доступ к ресурсам, которые являются локальными. В этом разделе показывает способ подключения логики приложения tooan на локальной системе SAP. В этом примере логика приложения запрашивает IDOC по протоколу HTTP и отправляет ответ hello.    

> [!NOTE]
> Текущие ограничения: 
> - Приложения логики времени ожидания, если все действия, необходимые для ответа hello не завершается в течение hello [предельное время ожидания запроса](./logic-apps-limits-and-config.md). В этом сценарии запросы могут быть заблокированы. 
> - Средство выбора файлов Hello не отображает все доступные поля hello. В этом случае пути можно добавить вручную.

## <a name="prerequisites"></a>Предварительные требования

- Установка и настройка hello последней [локального шлюза данных](https://www.microsoft.com/download/details.aspx?id=53127) версии 1.15.6150.1 или более поздней версии. [Как tooconnect toohello локальный шлюз данных в приложении логику](http://aka.ms/logicapps-gateway) списки hello действия. шлюз Hello должны устанавливаться на локальном компьютере, прежде чем продолжить.

- Загрузки и установки hello последнюю SAP клиентскую библиотеку на hello же компьютер, где установлен шлюз данных hello. Выполните одно из следующих версий SAP hello. 
    - SAP Server
        - Любой сервер SAP, поддержка hello соединитель .NET (NCo) 3.0
 
    - SAP Client
        - Соединитель SAP .NET (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>Добавление триггеров и действий для подключения системы SAP tooyour

Соединитель SAP Hello имеет действия, но не триггеры. Таким образом у нас есть toouse срабатывание другого триггера в начале hello hello рабочего процесса. 

1. Добавить триггер hello запросов и ответов, а затем выберите **новый шаг**.

2. Выберите **добавить действие**, а затем выберите соединитель SAP hello, введя `SAP` в поле поиска hello:    

     ![Выберите сервер приложений SAP или сервер сообщений SAP](media/logic-apps-using-sap-connector/sap-action.png)

3. Выберите [**сервер приложений SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) или [**сервер сообщений SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm) в зависимости от конфигурации SAP. Если у вас нет существующего подключения, не запрошенные toocreate один.

   1. Выберите **подключиться через локальный шлюз данных**и введите сведения о hello для вашей системы SAP:   

       ![Добавить tooSAP строки подключения](media/logic-apps-using-sap-connector/picture2.png)  

   2. В разделе **шлюза**выберите существующий шлюз или tooinstall новый шлюз, выберите **установить шлюз**.

        ![Установка нового шлюза](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. После ввода всех сведений о hello выберите **создать**. 
   Логика приложения настраивает и проверяет hello подключения, убедившись, что hello подключение работает правильно.

4. Введите имя для подключения SAP.

5. Теперь доступны различные варианты SAP Hello. toofind категории IDOC, выберите из списка hello. Или вручную ввести путь hello и выберите hello HTTP-ответ в hello **текст** поля:

     ![Действие SAP](media/logic-apps-using-sap-connector/picture3.png)

6. Добавить действие hello для создания **HTTP-ответа**. приветственное сообщение ответа должно быть из выходных данных SAP hello.

7. Сохраните приложение логики. Протестируйте его путем отправки IDOC через URL-адрес триггера hello HTTP. После отправки IDOC приветствия ожидание hello ответа от приложения hello логики:   

     > [!TIP]
     > Узнать о возможностях слишком[Отслеживайте свои приложения логики](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Теперь, когда соединитель SAP hello добавляется tooyour логику приложения, отправной точкой для других функций:

- BAPI
- RFC

## <a name="get-help"></a>Получение справки

вопросы tooask ответить на вопросы и узнайте, какие другие логику приложения Azure пользователи делают, посетите hello [форуме по Azure логику приложений](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp улучшить логику приложения Azure и соединителей, проголосовать или отправить идеями hello [веб-сайт отзывов пользователей приложения логики Azure](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, как toovalidate, преобразования и других функций, аналогичных BizTalk в hello [пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md). 
- [Подключение к данным локальной tooon](../logic-apps/logic-apps-gateway-connection.md) из приложений логики
