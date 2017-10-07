---
title: "устройство StorSimple 8000 tootroubleshoot средство aaaDiagnostics | Документы Microsoft"
description: "Описание режимов устройства StorSimple hello и как toouse Windows PowerShell для StorSimple toochange hello режим устройства."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a>Используйте hello средство диагностики StorSimple tootroubleshoot 8000 ряда проблем устройствами

## <a name="overview"></a>Обзор

Средство диагностики StorSimple Hello Диагностика toosystem связанных проблем, производительности, сети и работоспособность компонента оборудования для устройства StorSimple. Средство диагностики Hello может использоваться в различных сценариях. К таким сценариям относятся рабочей нагрузки планирование, развертывание устройства StorSimple, оценки hello сетевой среды и определение hello производительность рабочего устройства. В этой статье содержится обзор средства диагностики hello и описано использование средства hello с устройством StorSimple.

Средство диагностики Hello в основном предназначен для локальных устройств серии StorSimple 8000 (8100 и 8600).

## <a name="run-diagnostics-tool"></a>Запуск средства диагностики

Это средство можно запускать при помощи hello в интерфейсе Windows PowerShell устройства StorSimple. Tooaccess hello локальный интерфейс устройства двумя способами:

* [Последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
* [Удаленный доступ к hello средство через hello Windows PowerShell для StorSimple](storsimple-remote-connect.md).

В этой статье предполагается, что вы подключились последовательной консоли устройства toohello через PuTTY.

#### <a name="toorun-hello-diagnostics-tool"></a>Средство диагностики toorun hello

После подключения toohello интерфейс Windows PowerShell устройства hello выполните следующие шаги toorun hello командлет hello.
1. Войдите на последовательную консоль устройства toohello, следуя указаниям hello [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).

2. Введите следующую команду hello:

    `Invoke-HcsDiagnostics`

    Если параметр области hello не указан, командлет hello выполняет все диагностические тесты hello. (проверка системы, работоспособности компонента оборудования, сети и производительности). 
    
    toorun только конкретного теста, укажите параметр области hello. Например toorun только hello тестирование сети, тип

    `Invoke-HcsDiagnostics -Scope Network`

3. Выделите и скопируйте выходной hello из hello PuTTY окна в текстовый файл для дальнейшего анализа.

## <a name="scenarios-toouse-hello-diagnostics-tool"></a>Средство диагностики hello toouse сценариев

Используйте hello диагностики средство tootroubleshoot hello сети, производительности, система и оборудование работоспособности системы hello. Ниже приведено несколько сценариев.

* **Устройство не в сети.** Устройство StorSimple серии 8000 находится в автономном режиме. Однако из интерфейса Windows PowerShell hello, кажется, что оба контроллера hello доступны и запущены.
    * Это средство можно использовать toothen определить состояние сетевого hello.
         
         > [!NOTE]
         > Не используйте это средство tooassess производительности и сетевые параметры на устройстве перед регистрации hello (или настройка с помощью мастера установки). Имеет допустимый IP-адрес назначается toohello устройства во время установки и регистрации. Этот командлет можно выполнить на незарегистрированном устройстве для проверки работоспособности оборудования и системы. Используйте параметр области hello, например:
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* **Проблемы постоянного устройства** -вы испытываете проблемы устройства, которые кажутся toopersist. Например, сбой регистрации. Вы может также сталкивается устройства после hello устройство не будет успешно зарегистрирован и оперативной некоторое время.
    * В этом случае используйте это средство для предварительного устранения неполадок, прежде чем отправлять запрос на поддержку Майкрософт. Рекомендуется запустить этот инструмент и отслеживания hello выходные данные этого средства. Затем можно предоставить этот tooexpedite tooSupport вывода устранения неполадок.
    * В случае сбоев компонентов оборудования или кластера необходимо отправить запрос на поддержку.

* **Низкий уровень производительности устройства.** Устройство Your StorSimple медленно работает.
    * В этом случае используйте этот командлет с tooperformance набор параметров области. Анализ вывода hello. Облако hello получение задержки чтения и записи. Используйте hello сообщил задержки в качестве максимального достичь целевого объекта, учитывайте некоторые издержки hello внутренней обработки данных, а затем развернуть hello рабочих нагрузок в системе hello. Дополнительные сведения см. слишком[использовать hello сети тестирование tootroubleshoot устройства производительности](#network-test).


## <a name="diagnostics-test-and-sample-outputs"></a>Диагностическая проверка и пример выходных данных

### <a name="hardware-test"></a>Проверка оборудования

Этот тест определяет состояние hello hello компоненты оборудования, встроенного по USM hello и встроенного по диска hello, выполняемых в системе.

* Hello оборудования отчет — эти компоненты этого теста не удалось hello или не присутствуют в системе hello.
* Hello USM встроенного по диска встроенного по версии и передаются для контроллера 0 контроллер 1 hello и общих компонентов в системе. Полный список компонентов оборудования см. в следующих разделах:

    * [Список компонентов для основного корпуса устройства StorSimple](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [Список компонентов для корпуса EBOD устройства StorSimple](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> Если проверки оборудования hello сообщает неисправных компонентов [входа в запрос на обслуживание в службу технической поддержки Майкрософт](storsimple-contact-microsoft-support.md).

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a>Пример выходных данных проверки оборудования устройства серии 8100

Ниже приведен пример выходных данных устройства StorSimple 8100. В модели устройства 8100 hello hello корпусе отсутствует. Таким образом компоненты контроллера EBOD hello не фиксируются.

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a>Системная проверка

Этот тест сообщает сведения о системе hello, доступных обновлений hello, сведения о кластере hello и hello службы сведения для вашего устройства.

* сведения о системе Hello включает hello модель, серийный номер устройства, часовой пояс, состояние контроллера и для версии программного обеспечения hello в системе hello. hello toounderstand различных системных параметров сообщила о выходе hello go слишком[интерпретации сведений о системе](#appendix-interpreting-system-information).

* доступности обновлений Hello отчеты, доступны ли hello обычных и обслуживания режима и их имена связанных пакетов. Если `RegularUpdates` и `MaintenanceModeUpdates` , `false`, это означает, что hello обновления недоступны. Устройство находится в актуальном состоянии.
* сведения о кластере Hello сведения hello на различных логических компонентов всех групп кластера HCS hello и их соответствующие состояния. Если вы видите группы вне сети кластера в этом разделе отчета hello [обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md).
* сведения о службе Hello включает имена hello и состояния всех hello HCS и элементы конфигурации службы, работающие на вашем устройстве. Эта информация полезна для hello технической поддержки корпорации Майкрософт в устранении проблемы устройства hello.

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a>Пример выходных данных системной проверки устройства серии 8100

Ниже приведен пример выходных данных теста системы hello запускается на устройстве с 8100.

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a>Проверка сети

Этот тест проверяет hello состояния hello сетевых интерфейсов, порты, DNS и NTP подключения к серверу, SSL сертификат, учетные данные хранилища, серверы обновления toohello подключения и подключения прокси на устройстве StorSimple.

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a>Пример выходных данных проверки сети при включении только DATA0

Ниже приведен пример выходных данных устройства 8100 hello. Вы увидите в выходных данных hello:
* Включены и настроены только сетевые интерфейсы DATA0 и DATA1.
* ДАННЫЕ 2 – 5 не включены на портале hello.
* Конфигурация DNS-сервера Hello является допустимым и hello устройства могут подключаться с помощью hello DNS-сервера.
* также подходит Hello соединение с сервером NTP.
* Открыты порты 80 и 443. Тем не менее порт 9354 заблокирован. В зависимости от hello [требования к системе для сети](storsimple-system-requirements.md), требуется tooopen этот порт для связи шины службы hello.
* Hello сертификации SSL является допустимым.
* Hello устройство может подключиться toohello учетной записи хранилища: _myss8000storageacct_.
* серверы tooUpdate Hello подключение является допустимым.
* Hello веб-прокси не настроен на этом устройстве.

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a>Пример выходных данных проверки сети при включении DATA0 и DATA1

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a>тест производительности;

Этот тест сообщает производительность cloud hello через задержки чтения и записи hello облака для устройства. Это средство можно использовать tooestablish базовых показателей производительности hello облака, можно добиться с помощью StorSimple. Hello средство отчетов hello максимальной производительности (наилучший сценарий для чтения и записи задержки), которые можно получить для соединения.

Как средство hello сообщает максимальной производительности достижимая hello, мы используем hello сообщила о задержки чтения и записи цели при развертывании hello рабочих нагрузок.

Hello тест моделирует hello размеры больших двоичных объектов, связанные с типами hello другой том на устройстве hello. Обычные многоуровневые тома и их резервные копии, закрепленные локально, используют большие двоичные объекты на 64 КБ. Многоуровневые тома с архивацией используют большие двоичные объекты объемом 512 КБ. Если устройство имеет многоуровневого и локально закрепленного тома настраиваются только hello теста соответствующей too64 КБ большой двоичный объект будет выполняться размер данных.

toouse это средство, выполните следующие шаги hello:

1.  Сначала создайте сочетание многоуровневых томов и многоуровневых томов с архивацией. Это действие гарантирует, что средство hello выполняет тесты hello 64 КБ и 512 КБ размер большого двоичного объекта.

2. Используйте командлет hello, после создания и настройки hello тома. Тип:

    `Invoke-HcsDiagnostics -Scope Performance`

3. Запишите hello задержки чтения и записи, о которых сообщает анализатор hello. Этот тест может занять несколько минут toorun до того, как результаты hello.

4. Если значения задержек подключения hello в категории hello ожидаемого диапазона, то hello задержки, о которых сообщает анализатор hello можно использовать в качестве максимального достичь цели при развертывании hello рабочих нагрузок. Учитывайте некоторый запас на внутреннюю обработку данных.

    Средство диагностики hello высоки, сообщила hello задержки чтения и записи:

    1. Настройки аналитики хранилища для службы BLOB-объектов и анализ hello вывода toounderstand hello задержки для hello учетной записи хранилища Azure. Подробные инструкции см. слишком[Включение и Настройка аналитики хранилища](../storage/common/storage-enable-and-view-metrics.md). Если эти задержки также высокого уровня и сравним toohello чисел, полученный от hello средство диагностики StorSimple, должны toolog запрос на обслуживание в хранилище Azure.

    2. При низкой задержки учетной записи хранилища hello, обратитесь в службу tooinvestigate администратор вашей сети, выдает задержек в сети.

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a>Пример выходных данных проверки производительности устройства серии 8100

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a>Приложение: интерпретация системных сведений

Вот таблица какие hello сопоставить различные параметры Windows PowerShell, сведения о системе hello. 

| Параметр PowerShell    | Описание  |
|-------------------------|------------------|
| Идентификатор экземпляра             | С каждым контроллером связан уникальный идентификатор или GUID.|
| Имя                    | Hello понятное имя устройства hello, как настроить с помощью портала Azure hello во время развертывания устройства. Понятное имя по умолчанию Hello — серийный номер устройства hello. |
| Модель                   | модель Hello вашего устройства серии StorSimple 8000. Hello модели может быть 8100 или 8600.|
| SerialNumber            | серийный номер устройства Hello назначается на заводе hello, а не 15 символов. Например, 8600-SHX0991003G44HT:<br> 8600 — это модель устройства hello.<br>SHX — является hello производства узла.<br> 0991003 — определенный продукт; <br> G44HT hello, последние 5 цифр, увеличивается на единицу toocreate уникальные серийные номера. Набор может быть неупорядоченным.|
| TimeZone                | Hello часовой пояс устройства, настроенным в hello портал Azure во время развертывания устройства.|
| CurrentController       | Hello контроллер, подключенных toothrough hello интерфейс Windows PowerShell устройства StorSimple.|
| ActiveController        | контроллер Hello, активна на устройстве и управляет все операции сетевого и дискового hello. Это может быть контроллер 0 или 1.  |
| Controller0Status       | состояние Hello контроллер 0 на вашем устройстве. состояние контроллера Hello может быть обычный режим восстановления или недоступен.|
| Controller1Status       | Hello состояние контроллера 1 на вашем устройстве.  состояние контроллера Hello может быть обычный режим восстановления или недоступен.|
| SystemMode              | Здравствуйте, общее состояние устройства StorSimple. Состояние устройства Hello может быть обычный, обслуживания, или списания (соответствует toodeactivated в hello портал Azure).|
| FriendlySoftwareVersion | Hello понятное строка, соответствующая toohello версию программного обеспечения. Системы с обновлением 4 hello понятное программное обеспечение версии будет ряда обновления StorSimple 8000 4.0.|
| HcsSoftwareVersion      | версия программного обеспечения HCS Hello запущена на устройстве. Для экземпляра hello HCS программного обеспечения версии соответствующего tooStorSimple 8000 ряда обновления 4.0 является 6.3.9600.17820. |
| ApiVersion              | версия программного обеспечения Hello hello API Windows PowerShell устройства HCS hello.|
| VhdVersion              | версия программного обеспечения Hello hello заводского образа, hello устройства поставлялась вместе с. При сбросе значения по умолчанию устройств toofactory выполняется версии программного обеспечения.|
| OSVersion               | версия программного обеспечения операционной системы Windows Server hello, запущенного на устройстве hello Hello. устройство StorSimple Hello основывается на Windows Server 2012 R2, соответствующий too6.3.9600 hello.|
| CisAgentVersion         | версия Hello вашей конфигурации агента на устройстве StorSimple. Этот агент позволяет взаимодействовать со службой StorSimple Manager hello, запущенных в Azure.|
| MdsAgentVersion         | Hello версии соответствующего toohello Mds агент, работающий на устройстве StorSimple. Этот агент перемещает toohello данных наблюдения и диагностики службы (MDS).|
| Lsisas2Version          | Здравствуйте, соответствующие драйверы toohello LSI версии на устройстве StorSimple.|
| Capacity                | Hello общая емкость устройства hello в байтах.|
| RemoteManagementMode    | Указывает, могут ли устройство hello удаленное управление через его интерфейс Windows PowerShell. |
| FipsMode                | Указывает, включен ли режим США федеральным сведения обработки Standard (FIPS) hello на вашем устройстве. стандарт Hello FIPS 140 определяет утвержденные для использования системами нам федеральным правительством компьютера для защиты конфиденциальных данных hello алгоритмов шифрования. Для устройств с обновлением версии 4 или более поздней режим FIPS включен по умолчанию. |

## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения hello [синтаксис командлета Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).

* Дополнительные сведения о том, как слишком[устранения проблем развертывания](storsimple-troubleshoot-deployment.md) на устройстве StorSimple.
