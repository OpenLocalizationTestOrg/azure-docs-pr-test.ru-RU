---
title: "aaaTroubleshoot защиты от сбоев VMware или физическими tooAzure | Документы Microsoft"
description: "В этой статье описываются распространенные ошибки при репликации VMware машины hello и как tootroubleshoot их"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Устранение неполадок репликации виртуальной машины VMware или физического сервера в локальной среде
Вы можете получить определенные сообщения об ошибках при защите виртуальных машин VMware или физических серверов с помощью Azure Site Recovery. Этой статьи описаны некоторые из наиболее распространенных сообщений об ошибках, обнаружения, а также устранение неполадок tooresolve действия Здравствуйте, их.


## <a name="initial-replication-is-stuck-at-0"></a>Начальная репликация зависла на 0 %
Большинство сбоев hello начальной репликации, которые мы сталкиваемся с поддержкой, из-за проблем с tooconnectivity между исходного сервера к процессу сервера или сервера процесса-Azure.
В большинстве случаев вы можете самостоятельно устранять эти проблемы, выполните указанные ниже действия hello.

###<a name="check-hello-following-on-source-machine"></a>Установите флажок, hello на ИСХОДНОМ КОМПЬЮТЕРЕ
* Из командной строки для компьютера исходного сервера используйте Telnet tooping hello сервера обработки с https-порт (по умолчанию 9443), как показано ниже toosee, если существуют проблемы с сетевым подключением или порт брандмауэра, критические препятствия.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > Использовать Telnet, не использует подключение tootest PING.  Если Telnet не установлена, выполните список шагов hello [здесь](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Если не удается tooconnect Разрешить входящий порт 9443 на приветствия сервера обработки и установите флажок, если hello проблема по-прежнему завершает работу. В некоторых случаях, когда сервер обработки находился за промежуточной подсетью, именно это вызывало такую проблему.

* Проверьте состояние службы hello `InMage Scout VX Agent – Sentinel/OutpostStart` если он не выполняется» и «проверка hello проблема все еще существует.   
 
###<a name="check-hello-following-on-process-server"></a>Установите флажок, hello на сервер ОБРАБОТКИ

* **Проверьте, если сервер обработки активно внедряет tooAzure данных** 

С сервера обработки машины откройте диспетчер задач (нажмите сочетание клавиш Ctrl-Shift-Esc) hello. Перейдите на вкладку "Быстродействие" toohello и щелкните ссылку «Открыть монитор ресурсов». Из диспетчера ресурсов перейдите tooNetwork вкладки. Проверьте, отправляет ли файл cbengine.exe на вкладке "Процессы с сетевой активностью" большие объемы данных (в МБ).

![Включение репликации](./media/site-recovery-protection-common-errors/cbengine.png)

Если нет, выполните указанные ниже действия hello.

* **Проверьте, является ли процесс сервера может tooconnect больших двоичных объектов Azure**: выберите и установите hello «TCP-подключений» cbengine.exe tooview toosee, если отсутствует связь с URL-адреса процесса сервера tooAzure хранилища больших двоичных объектов.

![Включение репликации](./media/site-recovery-protection-common-errors/rmonitor.png)

Если нет, перейдите на панель tooControl > Проверьте службы, если hello следующие службы запущены и работают:

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Re) Запустите любой службе, не выполняется и проверьте, существует ли проблема hello.

* **Проверьте, является ли процесс сервера может tooconnect tooAzure общедоступный IP-адрес через порт 443**

Откройте hello последнюю CBEngineCurr.errlog из `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` и выполните поиск: 443 и подключения не удалась.

![Включение репликации](./media/site-recovery-protection-common-errors/logdetails1.png)

Если возникли проблемы, с сервера обработки командной строки, используйте telnet tooping к Azure общедоступный IP-адрес (маскироваться в над изображением) в hello CBEngineCurr.currLog через порт 443.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
Если не удается tooconnect, проверьте проблемы доступа hello в случае из-за toofirewall или прокси-сервера, как описано в следующем шаге.


* **Проверьте, если IP-адресом брандмауэр на сервер обработки не блокируют доступ**: при использовании правила IP-адресом брандмауэра на сервере hello Загрузите полный список hello Microsoft Azure Datacenter диапазоны IP-адресов из [здесь ](https://www.microsoft.com/download/details.aspx?id=41653) и добавить их конфигурации tooensure tooyour брандмауэр, делают возможным обмен данными tooAzure (и hello порта HTTPS (443)).  Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).

* **Проверьте, если брандмауэр на основе URL-адреса на сервер обработки не блокирует доступ**: при использовании URL-адрес на основе правила брандмауэра на сервере hello убедитесь hello следующие URL-адреса будут добавлены toofirewall конфигурации. 
     
  `*.accesscontrol.windows.net:`: используется для контроля доступа и управления удостоверениями;

  `*.backup.windowsazure.com:`: используется для передачи данных репликации и оркестрации;

  `*.blob.core.windows.net:`Используется для доступа к toohello учетной записи хранилища, в котором хранятся данные репликации

  `*.hypervrecoverymanager.windowsazure.com:`: используется для операций управления репликацией и оркестрации;

  `time.nist.gov`и `time.windows.com`: использовать toocheck синхронизации времени между системой и глобальное время.

URL-адреса для **облака Azure для государственных организаций**:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **Проверьте, не блокируют ли доступ параметры прокси-сервера на сервере обработки.**  При использовании прокси-сервер, убедитесь, что разрешает имя прокси-сервера hello hello DNS-сервером.
toocheck указано во время установки сервера конфигурации hello. Перейдите в раздел tooregistry

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Теперь убедитесь, что hello одинаковые параметры используются по данным toosend агента Azure Site Recovery.
Поиск Microsoft Azure Backup 

![Включение репликации](./media/site-recovery-protection-common-errors/mab.png)

Откройте службу и щелкните "Действие > Изменить свойства". На вкладке настройки прокси-сервера вы увидите адрес hello прокси-сервера, в который должны быть такими же, как показано hello реестра. Если нет, измените его toohello того же адреса.

![Включение репликации](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Проверьте, если на сервер обработки не ограничен регулирования пропускной способности**: увеличить пропускную способность hello и проверьте, существует ли проблема hello.

##<a name="next-steps"></a>Дальнейшие действия
Если вам нужна дополнительная помощь, разнесите запроса слишком[форум ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). У нас есть сообщество активно и один из наших инженеров будет может tooassist вы.
