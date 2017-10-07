---
title: "hello aaaUse соединитель Slack в свои приложения логики Azure | Документы Microsoft"
description: "Подключение tooSlack в свои приложения логики"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a>Начало работы с соединителем резерв hello
Slack — это средство для организации взаимодействия между группами пользователей, которое объединяет все сообщения в одном месте, поддерживает возможности мгновенного поиска и доступно в любом месте. 

Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tooslack"></a>Создание tooSlack подключения
Резерв соединителя toouse hello, сначала создать **подключения** затем укажите подробности hello для этих свойств: 

| Свойство | Обязательно | Description (Описание) |
| --- | --- | --- |
| Маркер |Да |Указание учетных данных Slack |

Выполните эти действия toosign в Slack, а полный hello конфигурация hello Slack **подключения** в приложении логики:

1. Выберите **Повторение**
2. Выберите **частоту** и введите **интервал**.
3. Выберите **Добавить действие**.  
   ![Настройка Slack][1]  
4. Введите в поле поиска hello резерв и дождитесь hello поиска tooreturn все записи со Slack в имени hello
5. Выберите **Slack — опубликовать сообщение**
6. Выберите **входа tooSlack**:  
   ![Настройка Slack][2]
7. Укажите ваш toosign резерв учетные данные в приложении tooauthorize hello    
   ![Настройка Slack][3]  
8. Вы будете страница входа на перенаправленном tooyour организации. **Авторизовать** резерв toointeract с логикой приложения:      
   ![Настройка Slack][5] 
9. После завершения авторизации hello вы будете перенаправленный tooyour логику приложения toocomplete его путем настройки hello **временных резервов - получение всех сообщений** раздела. Добавьте другие необходимые вам триггеры и действия.  
   ![Настройка Slack][6]
10. Сохранить результаты работы, выбрав **Сохранить** hello меню выше.

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/slack/).

## <a name="more-connectors"></a>Дополнительные сведения о соединителях
Вернитесь к предыдущему окну toohello [API-интерфейсы списка](apis-list.md).

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
