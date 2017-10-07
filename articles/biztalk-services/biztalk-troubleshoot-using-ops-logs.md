---
title: "с помощью журналов операций службы BizTalk aaaTroubleshoot | Документы Microsoft"
description: "Устранение неполадок в службах BizTalk с помощью журналов операций. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>Службы BizTalk: устранение неполадок с помощью журналов операций

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Что такое hello журналы операций
Журналы операций — это компонент служб управления, доступных в hello классический портал Azure, позволяющий tooview исторических журналы операций, выполняемых на службы Azure, включая службы BizTalk. Это позволяет tooview исторических данных связанных операций toomanagement в вашей подписке на службу BizTalk вплоть до 180 дней.

> [!NOTE]
> Эта функция только собирает журналы для операций управления на службы BizTalk, таких как запуска службы hello, резервные вверх, и т. д. Вне зависимости от того, является ли они выполняются на hello классический портал Azure или с помощью hello отслеживаются такие операции [API REST службы BizTalk](http://msdn.microsoft.com/library/azure/dn232347.aspx). Полный список операций, которые отслеживаются с помощью служб управления, см. в разделе [Операции, отслеживаемые с помощью служб управления Azure](#bizops).<br/><br/>
> Это не записываются журналы hello tooBizTalk связанные действия среда выполнения службы (например, сообщение, обрабатываемое мостов и т. д.). Эти журналы, tooview используйте hello представлении отслеживания из портала служб BizTalk hello. Дополнительные сведения см. в статье [Отслеживание сообщений](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>Просмотр журналов операций служб BizTalk
1. В hello классический портал Azure, выберите **службы управления**, а затем выберите hello **журналы операций** вкладку.
2. Можно фильтровать hello журналов, основанных на различные параметры, например подписки, диапазон дат, тип службы (например службы BizTalk), имя службы или состояние операции hello (успешно, сбой).
3. Выберите hello флажок tooview hello отфильтрованный список. Hello на рисунке показаны действия связанных tootestbiztalkservice: ![просматривать журналы операций][ViewLogs] 
4. Выберите строку hello tooview Дополнительные сведения о конкретной операции и нажмите кнопку **сведения** hello панели задач внизу hello.

## <a name="bizops"></a>Операции, отслеживаемые с помощью служб управления Azure
Hello следующей таблице перечислены операции hello, которые отслеживаются с помощью службы управления Azure hello.

| Имя операции | Задача |
| --- | --- |
| CreateBizTalkService |Операция toocreate новую службу BizTalk |
| DeleteBizTalkService |Операция toodelete службы BizTalk |
| RestartBizTalkService |Операция toorestart службы BizTalk |
| StartBizTalkService |Операция toostart службы BizTalk |
| StopBizTalkService |Операция toostop службы BizTalk |
| DisableBizTalkService |Операция toodisable службы BizTalk |
| EnableBizTalkService |Операция tooenable службы BizTalk |
| BackupBizTalkService |Tooback операции службы BizTalk |
| RestoreBizTalkService |Операция toorestore службу BizTalk из указанной резервной копии |
| SuspendBizTalkService |Операция toosuspend службы BizTalk |
| ResumeBizTalkService |Операция tooresume службы BizTalk |
| ScaleBizTalkService |Операция tooscale службы BizTalk вверх или вниз |
| ConfigUpdateBizTalkService |Операция tooupdate hello конфигурации службы BizTalk |
| ServiceUpdateBizTalkService |Tooupgrade операции или переход к более раннему tooa другая версия службы BizTalk |
| PurgeBackupBizTalkService |Резервные копии toopurge операции hello службы BizTalk за пределами срока хранения hello |

## <a name="see-also"></a>См. также
* [Резервное копирование службы BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Восстановление службы BizTalk из резервной копии](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Службы BizTalk. Диаграмма выпусков Developer, Basic, Standard и Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Службы BizTalk: подготовка с использованием классического портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Службы BizTalk. Диаграмма состояния подготовки](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Службы BizTalk: вкладки «Панель мониторинга», «Монитор» и «Масштаб»](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Службы BizTalk: регулирование](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Службы BizTalk: имя и ключ издателя](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Как я запустить с помощью hello пакета SDK служб BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

