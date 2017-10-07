---
title: "aaaLearn о регулирование в службах BizTalk | Документы Microsoft"
description: "Узнайте о пороговых значениях регулирования и соответствующем поведении среды выполнения для служб BizTalk. Регулирование основывается на использовании памяти и количестве сообщений. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a>Службы BizTalk: регулирование

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Службы BizTalk Azure реализует регулирование службы на основе двух условий: памяти использования и hello количество одновременных сообщений обработки. В этом разделе перечислены hello регулирования пороговых значений и описывает hello поведения во время выполнения при возникновении условия регулирования.

## <a name="throttling-thresholds"></a>Пороги регулирования
Привет, в следующей таблице перечислены hello регулирования источника и пороговых значений:

|  | Описание | Нижнее пороговое значение | Верхнее пороговое значение |
| --- | --- | --- | --- |
| Память |% всей доступной системной памяти/PageFileBytes (количество байтов файла подкачки). <p><p>Общее доступных PageFileBytes приблизительно — в два раза hello ОЗУ системы hello. |60 % |70 % |
| Обработка сообщений |Число сообщений, обрабатываемых одновременно |40 * число ядер |100 * число ядер |

При достижении верхнего порогового значения службы BizTalk Azure запускает toothrottle. Регулирование останавливается при достижении hello нижнее пороговое значение. Например, служба использует 65 % системной памяти. В этом случае служба hello не регулирование. Использование системной памяти повышается до 70 %. В этом случае служба hello регулирует и toothrottle продолжается, пока служба hello использует системную память 60% (нижнее пороговое значение).

Служб BizTalk Azure отслеживает hello регулирования состояния (нормальное состояние и состояние регулированию) и регулирования длительность hello.

## <a name="runtime-behavior"></a>Поведение во время выполнения
Когда службы BizTalk Azure переходит в состояние регулирования, происходит hello следующее:

* Регулирование осуществляется для отдельных экземпляров роли. Например:<br/>
  RoleInstanceA выполняет регулирование. RoleInstanceB не ведет регулирование. В этом случае сообщения в RoleInstanceB обрабатываются как ожидалось. Сообщения в RoleInstanceA отбрасываются и завершаться hello следующая ошибка:<br/><br/>
  **Сервер занят. Повторите попытку позже.**<br/><br/>
* Ни один запрашивающий источник не ведет опрос и не загружает сообщение. Например,<br/>
  конвейер извлекает сообщения из внешнего FTP-источника. экземпляр роли Hello выполнив hello запросу возвращает в состоянии регулирования. В этом случае конвейера hello останавливает загрузка дополнительных сообщений, пока экземпляр роли hello перестанет регулирования.
* Клиент toohello отправляется ответ, клиент hello можно повторно отправить сообщение hello.
* Дождитесь, пока не будет устранена регулирования hello. В частности необходимо дождаться, пока достигается hello нижнее пороговое значение.

## <a name="important-notes"></a>Важные примечания
* Регулирование нельзя отключить.
* Пороговые значения регулирования нельзя изменить.
* Регулирование реализуется на уровне всей системы.
* Hello сервера базы данных SQL Azure имеет встроенные регулирования.

## <a name="additional-azure-biztalk-services-topics"></a>Дополнительная информация о службах BizTalk в Azure
* [Установка пакета SDK служб BizTalk Azure hello](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Руководства по службам BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Как я запустить с помощью hello пакета SDK служб BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Службы BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>См. также
* [Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Службы BizTalk: подготовка с использованием классического портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Службы BizTalk. Диаграмма состояния подготовки](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Службы BizTalk: резервное копирование и восстановление](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Службы BizTalk: имя и ключ издателя](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

