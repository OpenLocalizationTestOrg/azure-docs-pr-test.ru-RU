---
title: "Устранение неполадок в Azure Наблюдатель сети tooresource aaaIntroduction | Документы Microsoft"
description: "Эта страница предоставляет общие сведения о возможности по устранению неполадок ресурсов Наблюдатель сети hello"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a>Устранение неполадок в Azure Наблюдатель сети tooresource введение

Шлюзы виртуальной сети обеспечивают связь между локальными ресурсами и другими виртуальными сетями в Azure. Мониторинг этих шлюзов и их соединения является критическим tooensuring связи не нарушена. Наблюдатель сети предоставляет возможность tootroubleshoot hello шлюзах виртуальной сети и подключения. Это может вызываться через портал hello, PowerShell, CLI или REST API. При вызове Наблюдатель сети Диагностика работоспособности hello hello шлюз виртуальной сети или подключений и соответствующие результаты возврата hello. Этот запрос является долго выполняющаяся транзакция, hello результатов после завершения диагностики hello.

![портал][2]

## <a name="results"></a>Результаты

Hello предварительные результаты, возвращаемые дают общее представление о работоспособности hello hello ресурса. Для ресурсов могут быть предоставлены подробные сведения, как показано в следующем разделе hello:

Hello ниже приведен hello значения, возвращаемые с hello устранения API.

* **время начала** -это значение равно времени hello hello Устранение неполадок запуска при вызове API.
* **время окончания** -это значение является время hello, завершения устранения неполадок hello.
* **code** — имеет значение UnHealthy в случае обнаружения отдельной ошибки при диагностике.
* **результаты** -результаты — это набор результатов, возвращаемый на hello соединения или hello шлюз виртуальной сети.
    * **Идентификатор** -это значение является типом ошибки hello.
    * **Сводка** -это значение представляет собой сводку ошибок hello.
    * **Подробные** -это значение содержит подробное описание ошибки hello.
    * **recommendedActions** -это свойство представляет собой коллекцию tootake рекомендуемые действия.
      * **actionText** -это значение содержит текст hello, описывающий какие tootake действие.
      * **actionUri** -это значение содержит hello URI toodocumentation tooact.
      * **actionUriText** -это значение является краткое описание действия текста hello.

Hello следующие таблицы Показать hello ошибок типы (идентификатор в области результатов из списка hello), доступных, и если hello сбоя журнала.

### <a name="gateway"></a>Шлюз

| Тип ошибки | Причина | Журнал|
|---|---|---|
| NoFault | Ошибка не обнаружена. |Да|
| GatewayNotFound | Не удается найти шлюз или шлюз не подготовлен. |Нет|
| PlannedMaintenance |  Выполняется обслуживание экземпляра шлюза.  |Нет|
| UserDrivenUpdate | Идет обновление, инициированное пользователем. Это может быть операция изменения размера. | Нет |
| VipUnResponsive | Не удается связаться с hello первичного экземпляра hello шлюза. Это происходит, когда происходит сбой проверки работоспособности hello. | Нет |
| PlatformInActive | Имеется проблема с платформой hello. | Нет|
| ServiceNotRunning | базовая служба Hello не выполняется. | Нет|
| NoConnectionsFoundForGateway | Подключения не существует в шлюзе hello. Это всего лишь предупреждение.| Нет|
| ConnectionsNotConnected | Подключения не установлены. Это всего лишь предупреждение.| Да|
| GatewayCPUUsageExceeded | текущее использование ЦП шлюза Hello равно > 95%. | Да |

### <a name="connection"></a>Подключение

| Тип ошибки | Причина | Журнал|
|---|---|---|
| NoFault | Ошибка не обнаружена. |Да|
| GatewayNotFound | Не удается найти шлюз или шлюз не подготовлен. |Нет|
| PlannedMaintenance | Выполняется обслуживание экземпляра шлюза.  |Нет|
| UserDrivenUpdate | Идет обновление, инициированное пользователем. Это может быть операция изменения размера.  | Нет |
| VipUnResponsive | Не удается связаться с hello первичного экземпляра hello шлюза. Это происходит, когда происходит сбой проверки работоспособности hello. | Нет |
| ConnectionEntityNotFound | Отсутствует конфигурация подключения. | Нет |
| ConnectionIsMarkedDisconnected | Hello соединение помечается как «отключенной». |Нет|
| ConnectionNotConfiguredOnGateway | Hello базовой службы не имеет настроенного подключения hello. | Да |
| ConnectionMarkedStandy | соответствующая служба Hello помечается как standby.| Да|
| Аутентификация | Несоответствие предварительного ключа. | Да|
| PeerReachability | Hello одноранговых шлюз недоступен. | Да|
| IkePolicyMismatch | Hello одноранговых шлюза имеет IKE политики, которые не поддерживаются в Azure. | Да|
| WfpParse Error | Ошибка синтаксического анализа журнала WFP hello. |Да|

## <a name="supported-gateway-types"></a>Поддерживаемые типы шлюзов

Hello ниже перечислены hello поддержки показано, какие шлюзы и подключения поддерживаются в устранении неполадок Наблюдатель сети.
|  |  |
|---------|---------|
|**Типы шлюзов**   |         |
|Виртуальная частная сеть      | Поддерживаются        |
|ExpressRoute | Не поддерживается |
|Hypernet | Не поддерживается|
|**Типы VPN** | |
|На основе маршрутов | Поддерживаются|
|На основе политик | Не поддерживается|
|**Типы подключений**||
|IPsec| Поддерживаются|
|Vnet2Vnet| Поддерживаются|
|ExpressRoute| Не поддерживается|
|Hypernet| Не поддерживается|
|VPNClient| Не поддерживается|

## <a name="log-files"></a>Файлы журналов

файлы журнала устранения неполадок Hello ресурсов хранятся в учетной записи хранения, после завершения устранения неполадок ресурсов. Hello на иллюстрации показан пример hello содержимое вызова, который завершился ошибкой.

![ZIP-файл][1]

> [!NOTE]
> В некоторых случаях только подмножество hello файлы журналов записывается toostorage.

Инструкции по загрузке файлов из учетных записей хранилища azure, см. в разделе слишком[приступить к работе с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Кроме того, можно использовать такое средство, как Storage Explorer. Дополнительные сведения об обозревателе хранилища можно найти по ссылке hello здесь: [обозреватель хранилищ](http://storageexplorer.com/)

### <a name="connectionstatstxt"></a>ConnectionStats.txt

Hello **ConnectionStats.txt** файл содержит общую статистику hello соединения, включая байты входящего и исходящего состояние подключения и подключения hello время hello.

> [!NOTE]
> Если toohello вызов hello, устранение неполадок API возвращает работоспособное, hello единственное возвращается в hello ZIP-файл — **ConnectionStats.txt** файла.

содержимое этого файла Hello, аналогичные toohello следующий пример:

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a>CPUStats.txt

Hello **CPUStats.txt** файл содержит ЦП и памяти, доступной во время hello тестирования.  Hello этот файл содержит аналогичные toohello следующий пример:

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a>IKEErrors.txt

Hello **IKEErrors.txt** файл содержит ошибки, найденные во время мониторинга IKE.

Hello следующем примере показано содержимое файла IKEErrors.txt hello. Ошибки могут отличаться в зависимости от проблемы hello.

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a>Scrubbed-wfpdiag.txt

Hello **Scrubbed wfpdiag.txt** файл журнала содержит журнал wfp hello. В этом журнале регистрируется удаление пакетов, а также сбои протокола IKE и AuthIP.

Hello пример hello содержимое файла Scrubbed wfpdiag.txt hello. В этом примере hello общего ключа соединения не был правильно, как видно из 3-й строки hello снизу hello. Следующий пример Hello — просто фрагмент кода hello всего журнала, как hello журнал может быть длительное время, в зависимости от проблемы hello.

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a>wfpdiag.txt.sum

Hello **wfpdiag.txt.sum** файл является журнал, содержащий буферов hello и обработанных событий.

Hello следующий пример — содержимое файла wfpdiag.txt.sum hello.
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как toodiagnose VPN-шлюзы и подключения через hello портала, посетив [Устранение неполадок шлюза - портал Azure](network-watcher-troubleshoot-manage-portal.md).
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
