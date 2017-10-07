---
title: "aaaAdministration и список задач разработки в службах BizTalk | Документы Microsoft"
description: "Планирование и инструкции по развертыванию служб BizTalk Azure"
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: 0ab70b5b-1a88-4ba5-b329-ec51b785010e
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: 544c6b23fcbc2267598b713dbe1626699099d181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="administration-and-development-task-list-in-biztalk-services"></a>Список задач администрирования и разработки в службах BizTalk

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="getting-started"></a>Приступая к работе
При работе со службами Microsoft Azure BizTalk, существует несколько локальных и облачных компонентов tooconsider. tooget работу, примите во внимание hello следующий процесс.  

| Шаг | Ответственное лицо | Задача | Связанные ссылки |
| --- | --- | --- | --- |
| 1. |Администратор |Создать hello подписка Microsoft Azure с помощью учетной записи Майкрософт или учетной записи организации |[классическом портале Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885) |
| 2. |Администратор |Создание или подготовка службы BizTalk. |[Создание службы BizTalk с помощью классического портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) |
| 3. |Администратор |Регистрация развертывания службы BizTalk, принадлежащего вам или вашей компании. |[Регистрация и обновление развертывания службы BizTalk на портале служб BizTalk hello](https://msdn.microsoft.com/library/azure/hh689837.aspx) |
| 4. |Администратор |Применяется, если приложение hello использует Line of Business (LOB) в локальной системе для службы адаптера BizTalk tooconnect tooan или использует назначение очереди или раздела.  Создайте пространство имен шины обслуживания Azure hello. Предоставьте это пространство имен, имя издателя шины обслуживания и developer toohello значения ключа издателя шины службы. |[Практическое руководство. Создание или изменение пространства имен службы служебной шины](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md) и [Получение значений имени поставщика и ключа поставщика](biztalk-issuer-name-issuer-key.md) |
| 5. |Developer |Установите пакет SDK для hello и создайте hello проекта службы BizTalk в Visual Studio. |[Установка пакета SDK для служб Azure BizTalk](https://msdn.microsoft.com/library/azure/hh689760.aspx) и [Создание конечных точек расширенного обмена сообщениями в Azure](https://msdn.microsoft.com/library/azure/hh689766.aspx) |
| 6. |Developer |Развертывание вашей tooyour проекта службы BizTalk, размещенной службы BizTalk в Azure. |[Развертывание и обновление hello проекта служб BizTalk](https://msdn.microsoft.com/library/azure/hh689881.aspx) |
| 7. |Администратор |Применяется, если вы используете EDI.  Можно добавлять партнеров и создавать соглашения hello портале служб BizTalk Microsoft Azure. При создании соглашения можно добавить мост hello и/или преобразования, созданные параметры соглашения toohello разработчика hello. |[Настройка EDI, AS2 и EDIFACT на портале служб BizTalk](https://msdn.microsoft.com/library/azure/hh689853.aspx) |
| 8. |Администратор |С помощью hello классический портал Azure, для отслеживания работоспособности hello службы BizTalk, включая показатели производительности. |[Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»](http://go.microsoft.com/fwlink/p/?LinkID=302281) |
| 9. |Администратор |Управлять hello артефактами, используемыми служб BizTalk и отслеживание сообщений, обрабатываемых файлов моста hello hello портале служб BizTalk Microsoft Azure. |[С помощью hello портале служб BizTalk](https://msdn.microsoft.com/library/azure/dn874043.aspx) |
| 10. |Администратор |Создайте план резервного копирования tooback копирование hello службы BizTalk. |[Непрерывность бизнес-процессов и аварийное восстановление в службах BizTalk](https://msdn.microsoft.com/library/azure/dn509557.aspx) |

## <a name="next-steps"></a>Дальнейшие действия
[Учебники и примеры](https://msdn.microsoft.com/library/azure/hh689895.aspx)

[Создание проекта hello в Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)

[Установка пакета SDK служб BizTalk Azure](https://msdn.microsoft.com/library/azure/hh689760.aspx)

## <a name="concepts"></a>Основные понятия
[Создание проекта hello в Visual Studio](https://msdn.microsoft.com/library/azure/hh689811.aspx)  
[EDI, AS2 и EDIFACT обмена сообщениями (Business tooBusiness)](https://msdn.microsoft.com/library/azure/hh689898.aspx)  

## <a name="other-resources"></a>Другие ресурсы
[Добавление конечных точек источника, назначения и моста](https://msdn.microsoft.com/library/azure/hh689877.aspx)  
[Обучение и создание сопоставлений и преобразований сообщений](https://msdn.microsoft.com/library/azure/hh689905.aspx)  
[С помощью hello службы адаптера BizTalk (BAS)](https://msdn.microsoft.com/library/azure/hh689889.aspx)  
[Службы BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)

